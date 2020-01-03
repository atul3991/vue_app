<template>
    <div class="box">
        <br/>
        <select name="clients" v-model="selected" @change="onChange($event)">
            <option>--Choose a Client--</option>
            <option v-for="data in clientsJson" :key="data.client_id" :value="data.client_id">{{data.client_name}}</option>
        </select>
        <br/>
        <br/>
        <roles :rolesData="rolesData" :clientId="clientId" v-if="showRoles"/>
        <br/>
    </div>
</template>

<script>
import roles from '@/components/Roles.vue'
import Component from 'vue-class-component';
export default {
    data(){
        return {
            clientsJson: JSON.parse(localStorage.getItem('clients')),
            selected: '--Choose a Client--',
            showRoles: false,
            rolesData: [],
            clientId: 0
        }
    },
    components: {
        roles
    },
    methods: {
        onChange(event) {
            this.showRoles = true;
            this.clientId = this.selected;
            this.rolesData = JSON.parse(localStorage.getItem('parentRolesGroup'))[this.selected];
        }
    }
}
</script>
<style>
.box select {
  padding: 12px;
  width: 250px;
  border: none;
  font-size: 14px;
  box-shadow: 0 5px 25px rgba(0, 0, 0, 0.2);
  -webkit-appearance: button;
  outline: none;
  cursor:pointer;
}
</style>