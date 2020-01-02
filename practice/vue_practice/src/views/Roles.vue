<template>
    <div class="roles"> 
        <h1>Roles Admin Page </h1>
        <dispRoles />
    </div>
</template>


<script>
import dispRoles from '@/components/display_roles.vue'
var clients = [{
    "client_id": 101,
    "client_name": "Optoro"
},
{
    "client_id": 102,
    "client_name": "Ikara"
},
{
    "client_id": 103,
    "client_name": "Ariat"
},
{
    "client_id": 104,
    "client_name": "XYZ"
}];
var parentRolesGroup = {
    101:[{
        "parent_role_group_id": 1001,
        "parent_role_group_name": "Client",
        "role_groups": [{
            "role_group_id": 100001,
            "role_group_name": "Client Admin",
            "roles":[{
                "role_name": "Read access",
                "role_id": 200001,
                "display": true
            },
            {
                "role_name": "Edit access",
                "role_id": 200002,
                "display": true
            },
            {
                "role_name": "Create access",
                "role_id": 200003,
                "display": true
            },
            {
                "role_name": "Delete access",
                "role_id": 200004,
                "display": true
            },
            {
                "role_name": "Approval access",
                "role_id": 200005,
                "display": true
            }]
        },
        {
            "role_group_id": 100002,
            "role_group_name": "Warehouse Admin",
            "roles":[{
                "role_name": "Operational access",
                "role_id": 200006,
                "display": true
            },
            {
                "role_name": "Report access",
                "role_id": 200007,
                "display": true
            },
            {
                "role_name": "Managerial access",
                "role_id": 200008,
                "display": true
            },
            {
                "role_name": "Database access",
                "role_id": 200009,
                "display": true
            },
            {
                "role_name": "Update stock access",
                "role_id": 200010,
                "display": true
            }]
        },
        {
            "role_group_id": 100003,
            "role_group_name": "Account Admin",
            "roles":[{
                "role_name": "Add user",
                "role_id": 200011,
                "display": true
            },
            {
                "role_name": "Delete user",
                "role_id": 200012,
                "display": true
            },
            {
                "role_name": "Update user",
                "role_id": 200013,
                "display": true
            },
            {
                "role_name": "Read user",
                "role_id": 200014,
                "display": true
            }]
        },
        {
            "role_group_id": 100004,
            "role_group_name": "Catalogue Admin",
            "roles":[{
                "role_name": "Stocks manager",
                "role_id": 200015,
                "display": true
            },
            {
                "role_name": "Update Catalogue",
                "role_id": 200016,
                "display": true
            },
            {
                "role_name": "View Catalogue",
                "role_id": 200017,
                "display": true
            },
            {
                "role_name": "Delete Catalogue",
                "role_id": 200018,
                "display": true
            },
            {
                "role_name": "Share Catalogue",
                "role_id": 200019,
                "display": true
            },
            {
                "role_name": "Create Catalogue",
                "role_id": 200020,
                "display": true
            }]
        }]
    },
    {
        "parent_role_group_id": 1003,
        "parent_role_group_name": "Test",
        "role_groups": [{
            "role_group_id": 100021,
            "role_group_name": "Test Admin",
            "roles":[{
                "role_name": "Read access",
                "role_id": 200099,
                "display": true
            }]
        }]
    }],
    102:[{
        "parent_role_group_id": 1006,
        "parent_role_group_name": "xxxxxx",
        "role_groups": [{
            "role_group_id": 100001,
            "role_group_name": "yyyyy",
            "roles":[{
                "role_name": "dfvfdv access",
                "role_id": 200001,
                "display": true
            },
            {
                "role_name": "dc d",
                "role_id": 200002,
                "display": true
            },
            {
                "role_name": "Create access",
                "role_id": 200003,
                "display": true
            },
            {
                "role_name": "Delete access",
                "role_id": 200004,
                "display": true
            },
            {
                "role_name": "Approval access",
                "role_id": 200005,
                "display": true
            }]
        },
        {
            "role_group_id": 100002,
            "role_group_name": "Warehouse Admin",
            "roles":[{
                "role_name": "Operational access",
                "role_id": 200006,
                "display": true
            },
            {
                "role_name": "Report access",
                "role_id": 200007,
                "display": true
            },
            {
                "role_name": "Managerial access",
                "role_id": 200008,
                "display": true
            },
            {
                "role_name": "Database access",
                "role_id": 200009,
                "display": true
            },
            {
                "role_name": "Update stock access",
                "role_id": 200010,
                "display": true
            }]
        },
        {
            "role_group_id": 100003,
            "role_group_name": "Account Admin",
            "roles":[{
                "role_name": "Add user",
                "role_id": 200011,
                "display": true
            },
            {
                "role_name": "Delete user",
                "role_id": 200012,
                "display": true
            },
            {
                "role_name": "Update user",
                "role_id": 200013,
                "display": true
            },
            {
                "role_name": "Read user",
                "role_id": 200014,
                "display": true
            }]
        },
        {
            "role_group_id": 100004,
            "role_group_name": "Catalogue Admin",
            "roles":[{
                "role_name": "Stocks manager",
                "role_id": 200015,
                "display": true
            },
            {
                "role_name": "Update Catalogue",
                "role_id": 200016,
                "display": true
            },
            {
                "role_name": "View Catalogue",
                "role_id": 200017,
                "display": true
            },
            {
                "role_name": "Delete Catalogue",
                "role_id": 200018,
                "display": true
            },
            {
                "role_name": "Share Catalogue",
                "role_id": 200019,
                "display": true
            },
            {
                "role_name": "Create Catalogue",
                "role_id": 200020,
                "display": true
            }]
        }]
    }]
};

var roles = [{
    "role_name": "Read access",
    "role_id": 200001
},
{
    "role_name": "Edit access",
    "role_id": 200002
},
{
    "role_name": "Create access",
    "role_id": 200003
},
{
    "role_name": "Delete access",
    "role_id": 200004
},
{
    "role_name": "Approval access",
    "role_id": 200005
},
{
    "role_name": "Operational access",
    "role_id": 200006 
},
{
    "role_name": "Report access",
    "role_id": 200007 
},
{
    "role_name": "Managerial access",
    "role_id": 200008 
},
{
    "role_name": "Database access",
    "role_id": 200009 
},
{
    "role_name": "Update stock access",
    "role_id": 200010 
},
{
    "role_name": "Add user",
    "role_id": 200011 
},
{
    "role_name": "Delete user",
    "role_id": 200012 
},
{
    "role_name": "Update user",
    "role_id": 200013 
},
{
    "role_name": "Read user",
    "role_id": 200014 
},
{
    "role_name": "Stocks manager",
    "role_id": 200015 
},
{
    "role_name": "Update Catalogue",
    "role_id": 200016 
},
{
    "role_name": "View Catalogue",
    "role_id": 200017 
},
{
    "role_name": "Delete Catalogue",
    "role_id": 200018 
},
{
    "role_name": "Share Catalogue",
    "role_id": 200019 
},
{
    "role_name": "Create Catalogue",
    "role_id": 200020 
},
{
    "role_name": "dfvfdv access",
    "role_id": 200021 
},
{
    "role_name": "dc d",
    "role_id": 200022
},
{
    "role_name": "Test1",
    "role_id": 200023
},
{
    "role_name": "Test2",
    "role_id": 200024
},
{
    "role_name": "Test3",
    "role_id": 200025
},
{
    "role_name": "Test4",
    "role_id": 200026
},
{
    "role_name": "Test5",
    "role_id": 200027
},
{
    "role_name": "Test6",
    "role_id": 200028
},
{
    "role_name": "Test7",
    "role_id": 200029
},
{
    "role_name": "Test8",
    "role_id": 200030
},
{
    "role_name": "Test9",
    "role_id": 200031
},
{
    "role_name": "Test10",
    "role_id": 200032
}];

localStorage.setItem('clients', JSON.stringify(clients));
localStorage.setItem('parentRolesGroup', JSON.stringify(parentRolesGroup));
localStorage.setItem('newRoleGroupId', 1000000001);
localStorage.setItem('roles', JSON.stringify(roles));
export default {
    name: "roles",
    components: {
        dispRoles
    }
}
</script>