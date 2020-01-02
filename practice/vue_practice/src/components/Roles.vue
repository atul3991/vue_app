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
                                <autocomplete :search.sync="newRole" :items="['Test1', 'Test2', 'Test3', 'Tesdcd', 'Tejbbhj', 'tgvvhgghv']"/>
                                <button v-on:click="addRoles(index, index2)">Add</button> &nbsp;
                                <button v-on:click="hideDiv(roleGroup.role_group_id)">Cancel</button>
                            </span>
                        </h3>
                        <ul id="roles_ul">
                            <li v-for="(roles, index3) in roleGroup.roles" :key="roles.role_id">
                                <span v-if="roles.display">
                                    <label :id="roles.role_id"> {{ roles.role_name}} </label>
                                    <button v-on:click="removeRole(index,index2, index3, roles)" style="outline:none; border: none; padding: 0; background: none; cursor:pointer;"><img src="../../images/delete_icon.png" height="14" width="14" /></button>
                                </span>
                            </li>
                        </ul>
                        <hr v-if="index == rolesData.length - 1 || index2 != parent.role_groups.length - 1"/>
                    </li>
                </ul>
                <hr v-if="index != rolesData.length - 1"/>
            </li>
        </ul>
        <br/>
        <button v-on:click="saveRoles(rolesToRemove)">Save</button> &nbsp;
        <button v-on:click="cancelRolesSave()">Cancel</button>
    </div>
</template>


<script>
import autocomplete from "@/components/autocomplete.vue"
export default {
    components:{
        autocomplete
    },
    data(){
        return{
            rolesToRemove:[],
            rolesArray:[],
            newRole:''
        }
    },
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
            this.rolesData=data[document.querySelector("select[name=clients]").value];
        },
        addRoles(index, index2) {
            debugger;
            var roles = JSON.parse(localStorage.getItem('roles'));
            var newRoleName = this.newRole;
            var isValidRole = false;
            for(var i=0; i<roles.length; i++) {
                if(roles[i].role_name == newRoleName) {
                    isValidRole = true;
                    var newRole = {
                        "role_id": roles[i].role_id,
                        "role_name": newRoleName,
                        "display": true
                    };
                    var data = JSON.parse(localStorage.getItem('parentRolesGroup'));
                    data[document.querySelector("select[name=clients]").value][index].role_groups[index2].roles.push(newRole);
                    localStorage.setItem('parentRolesGroup', JSON.stringify(data));
                    this.rolesData=data[document.querySelector("select[name=clients]").value];
                    this.newRole = "";
                    break;
                }
            }
            if(!isValidRole) {
                alert("Enter a valid Role...!!!");
            }
        },
        removeRole(index, index2, index3, roles) {
            this.rolesToRemove.push({
                "client_id": document.querySelector("select[name=clients]").value,
                "parent_role_group_index": index,
                "role_group_index": index2,
                "role_index": index3
            });
            this.rolesArray.push(roles);
            roles.display=false;
        },
        saveRoles(rolesToRemove) {
            var parentRolesGroup = JSON.parse(localStorage.getItem('parentRolesGroup'));
            for(var i=0; i<rolesToRemove.length; i++){
                parentRolesGroup[rolesToRemove[i].client_id][rolesToRemove[i].parent_role_group_index].role_groups[rolesToRemove[i].role_group_index].roles.splice([rolesToRemove[i].role_index],1)
            }
            localStorage.setItem('parentRolesGroup', JSON.stringify(parentRolesGroup));
        },
        cancelRolesSave() {
            if(this.rolesArray.length != 0 && confirm("Changes made will be lost. Do you wish to proceed? ")){
                this.rolesToRemove=[];
                for(var i=0; i<this.rolesArray.length; i++) {
                    this.rolesArray[i].display = true;
                }
                this.rolesArray = [];
            }
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