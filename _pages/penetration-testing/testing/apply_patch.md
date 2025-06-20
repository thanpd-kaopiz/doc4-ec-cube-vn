---
title: Thiết lập để kiểm thử không bị gián đoạn
permalink: /penetration-testing/testing/apply_patch
---
Ví dụ, trong quá trình kiểm thử, có thể xảy ra trường hợp người dùng đang thực hiện kiểm thử bảo mật bị xóa hoặc quyền truy cập trang bị thay đổi khiến không thể truy cập được nữa.
Để ngăn chặn điều này và đảm bảo kiểm thử ổn định, cần chỉnh sửa trực tiếp vào mã nguồn EC-CUBE.

[Xem toàn bộ file patch tại đây](/patches/testing.patch)

**Lưu ý:** Ngoài các chỉnh sửa này, khi kiểm thử các chức năng xóa, cần comment out `EntityManager::flush()` trong các xử lý liên quan để đảm bảo thao tác xóa được rollback.
{: .notice--warning}

## Màn hình quản trị

### Ngăn chặn xóa quy cách, phân loại quy cách

``` diff
diff --git a/src/Eccube/Repository/ClassCategoryRepository.php b/src/Eccube/Repository/ClassCategoryRepository.php
index 8f08c2b9b2..4b4d9abdec 100644
--- a/src/Eccube/Repository/ClassCategoryRepository.php
+++ b/src/Eccube/Repository/ClassCategoryRepository.php
@@ -103,7 +103,7 @@ class ClassCategoryRepository extends AbstractRepository

         $em = $this->getEntityManager();
         $em->remove($ClassCategory);
-        $em->flush();
+        // $em->flush();
     }

     /**
diff --git a/src/Eccube/Repository/ClassNameRepository.php b/src/Eccube/Repository/ClassNameRepository.php
index 7e894b0585..4809d8262b 100644
--- a/src/Eccube/Repository/ClassNameRepository.php
+++ b/src/Eccube/Repository/ClassNameRepository.php
@@ -92,6 +92,6 @@ class ClassNameRepository extends AbstractRepository

         $em = $this->getEntityManager();
         $em->remove($ClassName);
-        $em->flush();
+        // $em->flush();
     }
 }
```

### Ngăn chặn logout

Khi logout, session sẽ bị ngắt và token CSRF sẽ thay đổi, dẫn đến kiểm thử thất bại. Vì vậy, cần vô hiệu hóa chức năng logout.

``` diff
diff --git a/app/config/eccube/packages/security.yaml b/app/config/eccube/packages/security.yaml
index 2ad4e1a608..8da71094d0 100644
--- a/app/config/eccube/packages/security.yaml
+++ b/app/config/eccube/packages/security.yaml
@@ -34,9 +34,9 @@ security:
                 use_forward: false
                 success_handler: eccube.security.success_handler
                 failure_handler: eccube.security.failure_handler
-            logout:
-                path: admin_logout
-                target: admin_login
+            # logout:
+            #     path: admin_logout
+            #     target: admin_login
         customer:
             pattern: ^/
             anonymous: true

```

### Ngăn chặn cập nhật quản lý quyền hạn

Nếu URL từ chối quyền hạn bị đăng ký là `/`, sẽ không thể truy cập màn hình quản trị. Cần ngăn chặn điều này.

```diff
diff --git a/src/Eccube/Controller/Admin/Setting/System/AuthorityController.php b/src/Eccube/Controller/Admin/Setting/System/AuthorityController.php
index 2f69bd5f62..4d2f4fdde1 100644
--- a/src/Eccube/Controller/Admin/Setting/System/AuthorityController.php
+++ b/src/Eccube/Controller/Admin/Setting/System/AuthorityController.php
@@ -103,7 +103,7 @@ class AuthorityController extends AbstractController
                     }
                 }
             }
-            $this->entityManager->flush();
+            // $this->entityManager->flush();

             $event = new EventArgs(
                 [

```

### Ngăn chặn cập nhật master data

Ngăn chặn việc master data bị cập nhật không mong muốn, dẫn đến các chức năng không hoạt động.

```diff
diff --git a/src/Eccube/Controller/Admin/Setting/System/MasterdataController.php b/src/Eccube/Controller/Admin/Setting/System/MasterdataController.php
index 9b661031ab..a517b9a6ff 100644
--- a/src/Eccube/Controller/Admin/Setting/System/MasterdataController.php
+++ b/src/Eccube/Controller/Admin/Setting/System/MasterdataController.php
@@ -162,7 +162,7 @@ class MasterdataController extends AbstractController
                 }

                 try {
-                    $this->entityManager->flush();
+                    // $this->entityManager->flush();

                     $event = new EventArgs(
                         [

```

### Ngăn chặn cập nhật thông tin user quản trị

Ngăn chặn việc thay đổi mật khẩu hoặc ID của user đang kiểm thử.

```diff
diff --git a/src/Eccube/Controller/Admin/Setting/System/MemberController.php b/src/Eccube/Controller/Admin/Setting/System/MemberController.php
index d1f042f67a..0ce6235b77 100644
--- a/src/Eccube/Controller/Admin/Setting/System/MemberController.php
+++ b/src/Eccube/Controller/Admin/Setting/System/MemberController.php
@@ -188,7 +188,7 @@ class MemberController extends AbstractController
                 $Member->setPassword($encodedPassword);
             }

-            $this->memberRepository->save($Member);
+            // $this->memberRepository->save($Member);

             $event = new EventArgs(
                 [

```

### Ngăn chặn cập nhật quản lý bảo mật

Ngăn chặn việc thay đổi nội dung quản lý bảo mật khiến không thể truy cập màn hình quản trị.

```diff
diff --git a/src/Eccube/Controller/Admin/Setting/System/SecurityController.php b/src/Eccube/Controller/Admin/Setting/System/SecurityController.php
index d48b4f36b2..a658bbd33b 100644
--- a/src/Eccube/Controller/Admin/Setting/System/SecurityController.php
+++ b/src/Eccube/Controller/Admin/Setting/System/SecurityController.php
@@ -71,28 +71,28 @@ class SecurityController extends AbstractController
                 'ECCUBE_FORCE_SSL' => $data['force_ssl'] ? 'true' : 'false',
             ]);

-            file_put_contents($envFile, $env);
+            // file_put_contents($envFile, $env);

-            // Cập nhật URL màn hình quản trị. Nếu thay đổi thì logout và login lại.
-            $adminRoute = $this->eccubeConfig['eccube_admin_route'];
-            if ($adminRoute !== $data['admin_route_dir']) {
-                $env = StringUtil::replaceOrAddEnv($env, [
-                    'ECCUBE_ADMIN_ROUTE' => $data['admin_route_dir'],
-                ]);
+            // // Cập nhật URL màn hình quản trị. Nếu thay đổi thì logout và login lại.
+            // $adminRoute = $this->eccubeConfig['eccube_admin_route'];
+            // if ($adminRoute !== $data['admin_route_dir']) {
+            //     $env = StringUtil::replaceOrAddEnv($env, [
+            //         'ECCUBE_ADMIN_ROUTE' => $data['admin_route_dir'],
+            //     ]);

-                file_put_contents($envFile, $env);
+            //     file_put_contents($envFile, $env);

-                $this->addSuccess('admin.setting.system.security.admin_url_changed', 'admin');
+            //     $this->addSuccess('admin.setting.system.security.admin_url_changed', 'admin');

-                // Đăng xuất
-                $this->tokenStorage->setToken(null);
+            //     // Đăng xuất
+            //     $this->tokenStorage->setToken(null);

-                // Xóa cache
-                $cacheUtil->clearCache();
+            //     // Xóa cache
+            //     $cacheUtil->clearCache();

-                // Đăng nhập lại vào màn hình quản trị
-                return $this->redirect($request->getBaseUrl().'/'.$data['admin_route_dir']);
-            }
+            //     // Đăng nhập lại vào màn hình quản trị
+            //     return $this->redirect($request->getBaseUrl().'/'.$data['admin_route_dir']);
+            // }

             $this->addSuccess('admin.common.save_complete', 'admin');

```

## Màn hình front

### Ngăn chặn thay đổi thông tin hội viên

Ngăn chặn việc thay đổi thông tin hội viên khiến không thể đăng nhập lại.

``` diff
diff --git a/src/Eccube/Controller/Mypage/ChangeController.php b/src/Eccube/Controller/Mypage/ChangeController.php
index 70121e110c..1846b6fbe6 100644
--- a/src/Eccube/Controller/Mypage/ChangeController.php
+++ b/src/Eccube/Controller/Mypage/ChangeController.php
@@ -97,7 +97,7 @@ class ChangeController extends AbstractController
                     $encoder->encodePassword($Customer->getPassword(), $Customer->getSalt())
                 );
             }
-            $this->entityManager->flush();
+            // $this->entityManager->flush();

             log_info('Hoàn thành chỉnh sửa hội viên');

```

### Ngăn chặn giới hạn số lượng địa chỉ nhận hàng

Ngăn chặn việc vượt quá số lượng địa chỉ nhận hàng tối đa khiến kiểm thử thất bại.

``` diff
diff --git a/src/Eccube/Controller/Mypage/DeliveryController.php b/src/Eccube/Controller/Mypage/DeliveryController.php
index af8dd653a6..803f3123f2 100644
--- a/src/Eccube/Controller/Mypage/DeliveryController.php
+++ b/src/Eccube/Controller/Mypage/DeliveryController.php
@@ -77,7 +77,7 @@ class DeliveryController extends AbstractController
             $addressCurrNum = count($Customer->getCustomerAddresses());
             $addressMax = $this->eccubeConfig['eccube_deliv_addr_max'];
             if ($addressCurrNum >= $addressMax) {
-                throw new NotFoundHttpException();
+                // throw new NotFoundHttpException();
             }
             $CustomerAddress = new CustomerAddress();
             $CustomerAddress->setCustomer($Customer);
```

### Ngăn chặn xóa thông tin địa chỉ nhận hàng

Ngăn chặn việc xóa thông tin địa chỉ nhận hàng khiến việc mua hàng thất bại.

```diff
diff --git a/src/Eccube/Controller/Mypage/DeliveryController.php b/src/Eccube/Controller/Mypage/DeliveryController.php
index f3ecbc1ed0..7bd7290c1a 100644
--- a/src/Eccube/Controller/Mypage/DeliveryController.php
+++ b/src/Eccube/Controller/Mypage/DeliveryController.php
@@ -170,7 +170,7 @@ class DeliveryController extends AbstractController
             throw new BadRequestHttpException();
         }

-        $this->customerAddressRepository->delete($CustomerAddress);
+        // $this->customerAddressRepository->delete($CustomerAddress);

         $event = new EventArgs(
             [

```

### Ngăn chặn thêm sản phẩm yêu thích

Ngăn chặn việc kiểm thử thêm sản phẩm yêu thích (`/products/add_favorite/<id>`) bị thất bại
*Không thể sử dụng đồng thời với patch ngăn chặn xóa sản phẩm yêu thích*

``` diff
diff --git a/src/Eccube/Repository/CustomerFavoriteProductRepository.php b/src/Eccube/Repository/CustomerFavoriteProductRepository.php
index 24430036a4..cff5db5a64 100644
--- a/src/Eccube/Repository/CustomerFavoriteProductRepository.php
+++ b/src/Eccube/Repository/CustomerFavoriteProductRepository.php
@@ -45,7 +45,7 @@ class CustomerFavoriteProductRepository extends AbstractRepository

             $em = $this->getEntityManager();
             $em->persist($CustomerFavoriteProduct);
-            $em->flush();
+            // $em->flush();
         }
     }
```

### Ngăn chặn xóa sản phẩm yêu thích

Ngăn chặn việc xóa sản phẩm yêu thích khiến kiểm thử liên quan đến sản phẩm yêu thích bị thất bại
*Không thể sử dụng đồng thời với patch ngăn chặn thêm sản phẩm yêu thích*

```diff
diff --git a/src/Eccube/Controller/Mypage/MypageController.php b/src/Eccube/Controller/Mypage/MypageController.php
index d3abe49efd..b02a841954 100644
--- a/src/Eccube/Controller/Mypage/MypageController.php
+++ b/src/Eccube/Controller/Mypage/MypageController.php
@@ -362,7 +362,7 @@ class MypageController extends AbstractController
         $CustomerFavoriteProduct = $this->customerFavoriteProductRepository->findOneBy(['Customer' => $Customer, 'Product' => $Product]);

         if ($CustomerFavoriteProduct) {
-            $this->customerFavoriteProductRepository->delete($CustomerFavoriteProduct);
+            // $this->customerFavoriteProductRepository->delete($CustomerFavoriteProduct);
         } else {
             throw new BadRequestHttpException();
         }

```

**Lưu ý:** Có thể kiểm thử luồng đăng ký→xóa bằng addon sequence
{: .notice--info}

### Ngăn chặn hội viên rút khỏi hệ thống

Ngăn chặn việc hội viên rút khỏi hệ thống khiến kiểm thử bị dừng lại

```diff
diff --git a/src/Eccube/Controller/Mypage/WithdrawController.php b/src/Eccube/Controller/Mypage/WithdrawController.php
index 796a0b943e..940709df9c 100644
--- a/src/Eccube/Controller/Mypage/WithdrawController.php
+++ b/src/Eccube/Controller/Mypage/WithdrawController.php
@@ -121,8 +121,8 @@ class WithdrawController extends AbstractController

                     // Chuyển sang trạng thái rút khỏi
                     $CustomerStatus = $this->customerStatusRepository->find(CustomerStatus::WITHDRAWING);
-                    $Customer->setStatus($CustomerStatus);
-                    $Customer->setEmail(StringUtil::random(60).'@dummy.dummy');
+                    //$Customer->setStatus($CustomerStatus);
+                    //$Customer->setEmail(StringUtil::random(60).'@dummy.dummy');

                     $this->entityManager->flush();

@@ -140,11 +140,11 @@ class WithdrawController extends AbstractController
                     $this->mailService->sendCustomerWithdrawMail($Customer, $email);

                     // Xóa session giỏ hàng và đơn hàng
-                    $this->cartService->clear();
-                    $this->orderHelper->removeSession();
+                    // $this->cartService->clear();
+                    // $this->orderHelper->removeSession();

                     // Đăng xuất
-                    $this->tokenStorage->setToken(null);
+                    // $this->tokenStorage->setToken(null);

                     log_info('Hoàn thành đăng xuất');

```

### Ngăn chặn đăng ký hội viên tạm thời

``` diff
diff --git a/src/Eccube/Controller/EntryController.php b/src/Eccube/Controller/EntryController.php
index 076ac0a991..30a089994a 100644
--- a/src/Eccube/Controller/EntryController.php
+++ b/src/Eccube/Controller/EntryController.php
@@ -180,7 +180,7 @@ class EntryController extends AbstractController
                         ->setPoint(0);

                     $this->entityManager->persist($Customer);
-                    $this->entityManager->flush();
+                    // $this->entityManager->flush();

                     log_info('Hoàn thành đăng ký hội viên');

```

### Ngăn chặn đăng ký hội viên chính thức

```
@@ -293,7 +293,7 @@ class EntryController extends AbstractController
         $CustomerStatus = $this->customerStatusRepository->find(CustomerStatus::REGULAR);
         $Customer->setStatus($CustomerStatus);
         $this->entityManager->persist($Customer);
-        $this->entityManager->flush();
+        // $this->entityManager->flush();

         log_info('Hoàn thành đăng ký hội viên chính thức');

```

### Không xóa giỏ hàng khi hoàn tất đơn hàng

Ngăn chặn việc xóa giỏ hàng khi hoàn tất đơn hàng.

*Việc chuyển từ màn hình xác nhận đơn hàng sang hoàn tất chỉ là POST token CSRF tới `/shopping/checkout`, nên có thể không quá hữu ích.*

``` diff
diff --git a/src/Eccube/Controller/ShoppingController.php b/src/Eccube/Controller/ShoppingController.php
index 8e99094d73..e8e744f39a 100644
--- a/src/Eccube/Controller/ShoppingController.php
+++ b/src/Eccube/Controller/ShoppingController.php
@@ -386,7 +386,7 @@ class ShoppingController extends AbstractShoppingController
                     return $response;
                 }

-                $this->entityManager->flush();
+                //$this->entityManager->flush();

                 log_info('[Xử lý đơn hàng] Đã hoàn thành xử lý đơn hàng.', [$Order->getId()]);
             } catch (ShoppingException $e) {
@@ -409,7 +409,7 @@ class ShoppingController extends AbstractShoppingController

             // Xóa giỏ hàng
             log_info('[Xử lý đơn hàng] Xóa giỏ hàng.', [$Order->getId()]);
-            $this->cartService->clear();
+            //$this->cartService->clear();

             // Gán ID đơn hàng vào session
             $this->session->set(OrderHelper::SESSION_ORDER_ID, $Order->getId());
@@ -417,7 +417,7 @@ class ShoppingController extends AbstractShoppingController
             // Gửi mail
             log_info('[Xử lý đơn hàng] Gửi mail đơn hàng.', [$Order->getId()]);
             $this->mailService->sendOrderMail($Order);
-            $this->entityManager->flush();
+            //$this->entityManager->flush();

             log_info('[Xử lý đơn hàng] Đã hoàn thành xử lý đơn hàng. Chuyển sang màn hình hoàn tất.', [$Order->getId()]);

@@ -463,7 +463,7 @@ class ShoppingController extends AbstractShoppingController
         }

         log_info('[Hoàn tất đơn hàng] Xóa session luồng mua hàng.');
-        $this->orderHelper->removeSession();
+        //$this->orderHelper->removeSession();

         $hasNextCart = !empty($this->cartService->getCarts());

```

### Gỡ bỏ giới hạn sử dụng plugin coupon

Cho phép sử dụng coupon lặp lại nhiều lần.

```
diff --git a/Controller/CouponShoppingController.php b/Controller/CouponShoppingController.php
index 7551217..091bbd7 100644
--- a/Controller/CouponShoppingController.php
+++ b/Controller/CouponShoppingController.php
@@ -159,7 +159,7 @@ class CouponShoppingController extends AbstractController
                     $form->get('coupon_cd')->addError(new FormError(trans('plugin_coupon.front.shopping.sameuser')));
                     $error = true;
                 }
-
+                $error = false;
                 // ----------------------------------
                 // Thêm mục giảm giá / Ghi đè tổng tiền
                 // ----------------------------------
```
