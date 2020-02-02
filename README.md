# LivePermissions
基于LiveData的权限申请库

使用方法：
```kotlin
LivePermissions(this).request(
                Manifest.permission.WRITE_EXTERNAL_STORAGE,
                Manifest.permission.READ_EXTERNAL_STORAGE,
                Manifest.permission.CAMERA
            ).observe(this, Observer {
                when (it) {
                    is PermissionResult.Grant -> {  //权限允许
                        Toast.makeText(this, "Grant", Toast.LENGTH_SHORT).show()
                    }
                    is PermissionResult.Rationale -> {  //权限拒绝
                        it.permissions.forEach {s->
                            println("Rationale:${s}")
                        }
                        Toast.makeText(this, "Rationale", Toast.LENGTH_SHORT)
                            .show()
                    }
                    is PermissionResult.Deny -> {   //权限拒绝，且勾选了不再询问
                        it.permissions.forEach {s->
                            println("deny:${s}")
                        }
                        Toast.makeText(this, "deny", Toast.LENGTH_SHORT).show()
                    }
                }
            })

```