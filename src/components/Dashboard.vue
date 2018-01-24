<template>
    <div id="dashboard">
        <h3>Dashboard</h3>

        <div class="fixed-action-btn">
            <router-link to="/new" class="btn-floating btn-larde red">
                <i class="fa fa-plus"></i>
            </router-link>
        </div>
    </div>
</template>
<script>
    export default {
        name: 'dashboard',
        data () {
            return {
                employees: []
            }
        },
        created () {
            
        },
        methods: {

        }

    }
</script>