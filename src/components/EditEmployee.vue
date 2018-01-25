<template>
    <div id="edit-employee">
        <h3>Edit Employee</h3>
        <div class="row">
            <form class="col s12" @submit.prevent="updateEmployee">
                <div class="row">
                    <div class="input-field col s12">
                        <input type="text" v-model="employee_id" required>
                        <!--<label>Employee ID#</label>-->
                    </div>
                </div>
                <div class="row">
                    <div class="input-field col s12">
                        <input type="text" v-model="name" required>
                        <!--<label>Name</label>-->
                    </div>
                </div>
                <div class="row">
                    <div class="input-field col s12">
                        <input type="text" v-model="dept" required>
                        <!--<label>Department</label>-->
                    </div>
                </div>
                <div class="row">
                    <div class="input-field col s12">
                        <input type="text" v-model="position" required>
                        <!--<label>Position</label>-->
                    </div>
                </div>
                <button class="btn" type="submit">Submit</button>
                <router-link to="/" class="btn grey">Cancel</router-link>
            </form>
        </div>
    </div>
</template>
<script>
    export default {
        name: 'edit-employee',
        data () {
            return {

            }
        }

    }
</script>