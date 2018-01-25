<template>
    <div id="view-employee">
        <ul class="collection with-header">
            <li class="collection-header">
                <h4> {{ name }}</h4>
            </li>
            <li class="collection-item">Employee ID# {{ employee_id }}</li>
            <li class="collection-item">Departament: {{ dept }}</li>
            <li class="collection-item">Position: {{ position }}</li>
        </ul>

        <router-link to="/" class="btn grey">Back</router-link>
        <button @click="deteteEmployee" class="btn red">Delete</button>

        <div class="fixed-action-btn">
            <router-link v-bind:to="{ name: 'edit-employee',params: {employee_id: employee_id}}"
                         class="btn-floating btn-larde red">
                <i class="fa fa-edit"></i>
            </router-link>
        </div>
    </div>
</template>
<script>
    import db from './firebaseInit'
    export default {
        name: 'view-employee',
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
            deteteEmployee () {
                if(confirm('Are you sure?')) {
                    db.collection('employees').where('employee_id','==',this.$route.params.employee_id).get().then(querySnapShot => {
                        querySnapShot.forEach(doc => {
                            doc.ref.delete()
                            this.$router.push('/')
                        })
                    })
                }
            }
        }

    }
</script>