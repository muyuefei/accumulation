# 权限管理设计

## RBAC模式
    * 用户表--users
    * 权限表--permissions
    * 角色表--roles
    * 角色表和权限表--role-permission
    * 用户和角色表--user-role


    users
    1. id   int
    2. name string
    3. email string
    4. password string
    5. create_time string
    6. update_time string
    7. status int (0: pause; 1: active; 2; pending)
    8. deleted bool

    roles
    1. id int
    2. title string
    3. description string

    user_role
    1. id int
    2. user_id int
    3. role_id int

    permissions
    1. id int
    2. title string
    3. description string
    4. slug string
    5. http_path string

    role-permission
    1. id int
    2. role_id int
    3. permission_id int

