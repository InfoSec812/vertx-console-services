<template>
    <div class="container-fluid">
        <div class="page-header">
            <h1>Services</h1>
        </div>
        <datatable :columns="tableColumns" :data="tableRows" filterable paginate></datatable>
    </div>
</template>

<script>
import Services from './services.js';

Services.initialize('/discovery');

import StatusLabel from './StatusLabel.vue';
import MetadataDisplay from './MetadataDisplay.vue';
import RegistrationText from './RegistrationText.vue';

export default {
    name: 'Services',
    mounted() {
        this.servicesCallback = services => this.tableRows = services;
        Services.addCallback(this.servicesCallback);
    },
    beforeDestroy() {
        Services.removeCallback(this.servicesCallback);
    },
    data() {
        return {
            tableColumns: [
                { label: 'Name', field: 'name' },
                { label: 'Type', field: 'type' },
                { label: 'Endpoint', field: 'location.endpoint' },
                { label: 'Registration', component: RegistrationText },
                { label: 'Status', component: StatusLabel },
                { label: 'Metadata', component: MetadataDisplay, cellClass: 'table-view-pf-actions' }
            ],
            tableRows: []
        }
    }
}
</script>
