<template>
    <div class="container">
        <div class="row mt-5">
            <div class="col-md-12">
                <div class="card">
                    <div class="card-header">
                        <h3 class="card-title">Users Table</h3>
                        <div class="card-tools">
                            <button class="btn btn-success" @click="newModal">Add New <i class="fa fa-user-plus fa-fw"></i></button>
                        </div>
                    </div>
                    <!-- /.card-header -->
                    <div class="card-body table-responsive p-0">
                        <table class="table table-hover">
                            <thead>
                                <tr>
                                    <th>ID</th>
                                    <th>Name</th>
                                    <th>Email</th>
                                    <th>Type</th>
                                    <th>Registered At</th>
                                    <th>Action</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr v-for="user in users.data" :key="user.id">
                                    <td>{{ user.id }}</td>
                                    <td>{{ user.name }}</td>
                                    <td>{{ user.email }}</td>
                                    <td>{{ user.type | ucFirst }}</td>
                                    <td>{{ user.created_at | dateFomat }}</td>
                                    <td>
                                        <a href="#" @click="editModal(user)">
                                            <i class="fas fa-edit blue"></i>
                                        </a>

                                        <a href="#" @click="deleteUser(user.id)">
                                            <i class="fa fa-trash red"></i>
                                        </a>
                                    </td>
                                </tr>
                                
                            </tbody>
                        </table>
                    </div>
                    <!-- /.card-body -->
                    <div class="card-footer">
                        <!-- <ul>
                            <li v-for="post in laravelData.data" :key="post.id">{{ post.title }}</li>
                        </ul> -->

                        <pagination :data="users" @pagination-change-page="getResults"></pagination>
                    </div>
                </div>
                <!-- /.card -->
            </div>
        </div>


        <!-- Add New Modal -->
        <div class="modal fade" id="addNew" tabindex="-1" role="dialog" aria-labelledby="addNewLabel" aria-hidden="true">
            <div class="modal-dialog modal-dialog-centered" role="document">
                <div class="modal-content">
                    <div class="modal-header">
                        <h5 v-show="!editMode" class="modal-title" id="addNewLabel">Add New User</h5>
                        <h5 v-show="editMode" class="modal-title" id="addNewLabel">Update User</h5>
                        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                        <span aria-hidden="true">&times;</span>
                        </button>
                    </div>
                    <form @submit.prevent="editMode ? updateUser() : createUser()">
                        <div class="modal-body">
                            
                            <div class="form-group">
                                <input v-model="form.name" type="text" name="name"
                                    class="form-control" :class="{ 'is-invalid': form.errors.has('name') }" placeholder="Name">
                                <has-error :form="form" field="name" ></has-error>
                            </div>

                            <div class="form-group">
                                <input v-model="form.email" type="email" name="email"
                                    class="form-control" :class="{ 'is-invalid': form.errors.has('email') }" placeholder="Email Address">
                                <has-error :form="form" field="email" ></has-error>
                            </div>

                            <div class="form-group">
                                <textarea v-model="form.bio" name="bio"
                                    placeholder="Short Bio for user(optional)"
                                    class="form-control" :class="{ 'is-invalid': form.errors.has('bio') }" >
                                </textarea>
                                <has-error :form="form" field="bio" ></has-error>
                            </div>
                            <div class="form-group">
                                <select v-model="form.type" name="type"
                                    class="form-control" :class="{ 'is-invalid': form.errors.has('type') }" >
                                    <option value="">Select a Role</option>
                                    <option value="admin">Admin</option>
                                    <option value="user">Standard User</option>
                                    <option value="auther">Author</option>
                                </select>
                                <has-error :form="form" field="type" ></has-error>
                            </div>

                            <div class="form-group">
                                <input v-model="form.password" type="password" name="password"
                                    placeholder="Password"
                                    class="form-control" :class="{ 'is-invalid': form.errors.has('password') }">
                                <has-error :form="form" field="password"></has-error>
                            </div>
                            
                        </div>
                        <div class="modal-footer">
                            <button type="button" class="btn btn-danger" data-dismiss="modal">Close</button>
                            <button v-show="!editMode" type="submit" class="btn btn-primary">Create</button>
                            <button v-show="editMode"  type="submit" class="btn btn-primary">Update</button>
                        </div>
                    </form>
                </div>
            </div>
        </div>
    </div>

</template>

<script>
import { setInterval } from 'timers';
    export default {
        data(){
            return {
                editMode: false,
                users: {

                },
                form: new Form({
                    id: '',
                    name: '',
                    email: '',
                    password:  '',
                    type: '',
                    bio: '',
                    photo: '' 
                })
            }
        },
        methods:{

            getResults(page = 1){
                axios.get('api/user?page=' + page)
				.then(response => {
					this.users = response.data;
				})
            },

            newModal(){
                this.editMode = false;
                this.form.reset();
                $('#addNew').modal('show');
            },
            updateUser()
            {
                this.$Progress.start();
                this.form.put('api/user/'+this.form.id)
                .then(() => {

                    $('#addNew').modal('hide');
                    swal.fire(
                        'Updated!',
                        'Your user has been updated.',
                        'success'
                    );
                    this.$Progress.finish();
                    Fire.$emit('AfterCreate');

                })
                .catch(() => {
                    this.$Progress.fail();
                });
            },
            editModal(user){
                this.editMode = true;
                this.form.reset();
                $('#addNew').modal('show');
                this.form.fill(user);
                this.form.clear();
            },
            loadUsers(){
                axios.get('api/user').then(({ data }) => (this.users = data));
            },
            createUser(){
                this.$Progress.start();
                this.form.post('api/user')
                .then(() => {
                    Fire.$emit('AfterCreate');
                    $('#addNew').modal('hide');

                    toast.fire({
                        type: 'success',
                        title: 'User created successfully!'
                    });

                    this.$Progress.finish();

                })
                .catch(() => {
                    this.$Progress.fail();
                });
                
            },

            deleteUser(id){
                swal.fire({
                    title: 'Are you sure?',
                    text: "You won't be able to revert this!",
                    type: 'warning',
                    showCancelButton: true,
                    confirmButtonColor: '#3085d6',
                    cancelButtonColor: '#d33',
                    confirmButtonText: 'Yes, delete it!'
                })
                .then((result) => {
                    //Send  request to the server
                    if (result.value) {
                        this.form.delete('api/user/'+id)
                        .then(() => {
                            
                                swal.fire(
                                    'Deleted!',
                                    'Your user has been deleted.',
                                    'success'
                                )

                            Fire.$emit('AfterCreate');

                        })
                        .catch(() => {
                            swal("Failed!", "There was something worng.", "warning");
                        });
                    }
                })
            },
        

        },
        created() {
            this.loadUsers();
            Fire.$on('AfterCreate', () => {
                this.loadUsers();
            });
        }
    }
</script>
