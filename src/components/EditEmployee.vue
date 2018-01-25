<template>
    <div id="edit-employee">
        <h3>Edit Employee</h3>
        <div class="row">
            <form class="col s12" @submit.prevent="updateEmployee">
                <div class="row">
                    <div class="input-field col s12">
                        <input type="text" v-model="employee_id" disabled>
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
    import db from './firebaseInit'
    export default {
        name: 'edit-employee',
        data () {
            return {
                employee_id: null,
                name: null,
                dept: null,
                position: null
            }
        },
        beforeRouteEnter (to, from, next) {
            db.collection('employees').where('employee_id','==',to.params.employee_id).get().then(querySnapShot => {
                querySnapShot.forEach(doc => {

                    next(vm => {
                        vm.employee_id = doc.data().employee_id
                        vm.name = doc.data().name
                        vm.dept = doc.data().DPT
                        vm.position = doc.data().position
                    })
                })
            })
        },
        wath: {
            '$route': 'fetchData'
        },
        methods: {
            fetchData () {
                db.collection('employees').where('employee_id','==',this.$route.params.employee_id).get().then(querySnapShot => {
                    querySnapShot.forEach(doc => {
                        this.employee_id = doc.data().employee_id
                        this.name = doc.data().name
                        this.dept = doc.data().dept
                        this.position = doc.data().position
                    })
                })
            },
            updateEmployee () {
                db.collection('employees').where('employee_id','==',this.$route.params.employee_id).get().then(querySnapShot => {
                    querySnapShot.forEach(doc => {
                        doc.ref.update({
                            employee_id: this.employee_id,
                            name: this.name,
                            dept: this.dept,
                            position: this.position
                        })
                            .then(() =>{
                                this.$router.push({
                                    name: 'view-employee',
                                    params: {employee_id: this.employee_id}
                                })
                            })
                    })
                })
            }
        }

    }
</script>