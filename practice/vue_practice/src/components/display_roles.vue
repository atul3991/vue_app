<template>
    <div>
        <br/>
        <select name="clients" v-model="selected" @change="onChange($event)">
            <option>--Choose a Client--</option>
            <option v-for="data in clientsJson" :key="data.client_id" :value="data.client_id">{{data.client_name}}</option>
        </select>
        <br/>
        <br/>
        <roles :rolesData="rolesData" v-if="showRoles"/>
        <br/>
    </div>
</template>

<script>
import roles from '@/components/Roles.vue'
import Component from 'vue-class-component';
var parentRolesGroup = JSON.parse(localStorage.getItem('parentRolesGroup'));
export default {
    data(){
        return {
            parentRolesGroupJson: JSON.parse(localStorage.getItem('parentRolesGroup')),
            clientsJson: JSON.parse(localStorage.getItem('clients')),
            selected: '--Choose a Client--',
            showRoles: false,
            rolesData: []
        }
    },
    components: {
        roles
    },
    methods: {
        onChange(event) {
            this.showRoles = true;
            this.rolesData = JSON.parse(localStorage.getItem('parentRolesGroup'))[document.querySelector("select[name=clients]").value];
        }
    }
}
</script>