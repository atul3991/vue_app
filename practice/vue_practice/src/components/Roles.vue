<template>
    <div>
        <ul>
            <li v-for="(parent, index) in rolesData" :key="parent.parent_role_group_id">
                <h2>
                    {{ parent.parent_role_group_name }} 
                    <button v-on:click="showDiv(parent.parent_role_group_id)" style="outline:none; border: none; padding: 0; background: none; cursor:pointer;"><img src="../../images/add_button.png" height="18" width="18" /></button>
                    <span :id="parent.parent_role_group_id" :ref="parent.parent_role_group_id" :hidden=true>
                        &nbsp;
                        <input :id="'new_role_group_'+index" type=text /> &nbsp;
                        <button v-on:click="addRolesGroup(index)">Add</button> &nbsp;
                        <button v-on:click="hideDiv(parent.parent_role_group_id)">Cancel</button>
                    </span>
                </h2>
                <ul>
                    <li v-for="(roleGroup, index2) in parent.role_groups" :key="roleGroup.role_group_id">
                        <h3>
                            {{ roleGroup.role_group_name }} 
                            <button v-on:click="showDiv(roleGroup.role_group_id)" style="outline:none; border: none; padding: 0; background: none; cursor:pointer;"><img src="../../images/add_button.png" height="16" width="16" /></button>
                            <span :id="roleGroup.role_group_id" :ref="roleGroup.role_group_id" :hidden=true>
                                &nbsp;
                                <input :id="'new_role_'+index2" type=text /> &nbsp;
                                <button v-on:click="addRoles(index, index2)">Add</button> &nbsp;
                                <button v-on:click="hideDiv(roleGroup.role_group_id)">Cancel</button>
                            </span>
                        </h3>
                        <ul id="roles_ul">
                            <li v-for="roles in roleGroup.roles" :key="roles.role_id">
                                <input type="checkbox" :id="roles.role_id">
                                <label for="roles.role_id"> {{ roles.role_name}} </label>
                            </li>
                        </ul>
                        <hr v-if="index == rolesData.length - 1 || index2 != parent.role_groups.length - 1"/>
                    </li>
                </ul>
                <hr v-if="index != rolesData.length - 1"/>
            </li>
        </ul>
        <br/>
        <button>Save</button> &nbsp;
        <button>Cancel</button>
    </div>
</template>


<script>
export default {
    props: ['rolesData'],
    methods: {
        showDiv(id) {
            this.$refs[id][0].hidden=false;
        },
        hideDiv(id) {
            this.$refs[id][0].hidden=true;
        },
        addRolesGroup(index) {
            var newRoleGroupId = JSON.parse(localStorage.getItem('newRoleGroupId'));
            var newRoleGroup = {
                "role_group_id": newRoleGroupId,
                "role_group_name": document.querySelector("input[id=new_role_group_"+index+"]").value,
                "roles": []
            };
            localStorage.setItem('newRoleGroupId', newRoleGroupId+1);
            var data = JSON.parse(localStorage.getItem('parentRolesGroup'));
            data[document.querySelector("select[name=clients]").value][index].role_groups.push(newRoleGroup);
            localStorage.setItem('parentRolesGroup', JSON.stringify(data));
        },
        addRoles(index, index2) {
            var newRoleId = JSON.parse(localStorage.getItem('newRoleId'));
            var newRole = {
                "role_id": newRoleId,
                "role_name": document.querySelector("input[id=new_role_"+index2+"]").value
            };
            localStorage.setItem('newRoleId', newRoleId+1);
            var data = JSON.parse(localStorage.getItem('parentRolesGroup'));
            data[document.querySelector("select[name=clients]").value][index].role_groups[index2].roles.push(newRole);
            localStorage.setItem('parentRolesGroup', JSON.stringify(data));
        }
    }
}
</script>
<style type="text/css">
div.ui-menu li {
    list-style:none;
    background-image:none;
    background-repeat:none;
    background-position:0; 
}
ul
{
    list-style-type:none;
    padding:0px;
    margin:0px;
}
li
{
    background-repeat:no-repeat;
    background-position:0px 5px; 
    padding-left:14px;
}
ul#roles_ul
{
    columns: 2;
    -webkit-columns: 2;
    -moz-columns: 2;
}
</style>