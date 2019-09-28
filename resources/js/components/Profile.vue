<template>
    <div class="container">
        <div class="row">
            <div class="col-md-12 mt-5">

                <div class="card card-widget widget-user">
                    <!-- Add the bg color to the header using any of the bg-* classes -->
                    <div class="widget-user-header text-white" style="background: url('./img/photo1.png') center center;">
                        <h3 class="widget-user-username text-center">{{ this.form.name }}</h3>
                        <h5 class="widget-user-desc text-center">{{ this.form.email }}</h5>
                    </div>
                    <div class="widget-user-image">
                        <img class="img-circle" :src="getProfilePhoto()" alt="User Avatar">
                    </div>
                    <div class="card-footer">
                        <div class="row">
                            <div class="col-sm-4 border-right">
                                <div class="description-block">
                                    <h5 class="description-header">3,200</h5>
                                    <span class="description-text">SALES</span>
                                </div>
                                <!-- /.description-block -->
                            </div>
                            <!-- /.col -->
                            <div class="col-sm-4 border-right">
                                <div class="description-block">
                                    <h5 class="description-header">13,000</h5>
                                    <span class="description-text">FOLLOWERS</span>
                                </div>
                                <!-- /.description-block -->
                            </div>
                            <!-- /.col -->
                            <div class="col-sm-4">
                                <div class="description-block">
                                    <h5 class="description-header">35</h5>
                                    <span class="description-text">PRODUCTS</span>
                                </div>
                                <!-- /.description-block -->
                            </div>
                            <!-- /.col -->
                        </div>
                        <!-- /.row -->
                    </div>
                </div>

                <div class="card">
                    <div class="card-header p-2">
                        <ul class="nav nav-pills">
                            <li class="nav-item"><a class="nav-link" href="#activity" data-toggle="tab">Activity</a></li>
                            <li class="nav-item"><a class="nav-link active" href="#settings" data-toggle="tab">Settings</a></li>
                        </ul>
                    </div>
                    <!-- /.card-header -->
                    <div class="card-body">
                        <div class="tab-content">
                            <div class="tab-pane" id="activity">
                                <!-- Post -->
                                <div class="post">
                                    <div class="user-block">
                                        <img class="img-circle img-bordered-sm" src="" alt="user image">
                                        <span class="username">
                                        <a href="#">Jonathan Burke Jr.</a>
                                        <a href="#" class="float-right btn-tool"><i class="fas fa-times"></i></a>
                                        </span>
                                        <span class="description">Shared publicly - 7:30 PM today</span>
                                    </div>
                                    <!-- /.user-block -->
                                    <p>
                                        Lorem ipsum represents a long-held tradition for designers,
                                        typographers and the like. Some people hate it and argue for
                                        its demise, but others ignore the hate as they create awesome
                                        tools to help create filler text for everyone from bacon lovers
                                        to Charlie Sheen fans.
                                    </p>
                                    <p>
                                        <a href="#" class="link-black text-sm mr-2"><i class="fas fa-share mr-1"></i> Share</a>
                                        <a href="#" class="link-black text-sm"><i class="far fa-thumbs-up mr-1"></i> Like</a>
                                        <span class="float-right">
                                        <a href="#" class="link-black text-sm">
                                        <i class="far fa-comments mr-1"></i> Comments (5)
                                        </a>
                                        </span>
                                    </p>
                                    <input class="form-control form-control-sm" type="text" placeholder="Type a comment">
                                </div>
                                <!-- /.post -->
                                <!-- Post -->
                                <div class="post clearfix">
                                    <div class="user-block">
                                        <img class="img-circle img-bordered-sm" src="" alt="User Image">
                                        <span class="username">
                                        <a href="#">Sarah Ross</a>
                                        <a href="#" class="float-right btn-tool"><i class="fas fa-times"></i></a>
                                        </span>
                                        <span class="description">Sent you a message - 3 days ago</span>
                                    </div>
                                    <!-- /.user-block -->
                                    <p>
                                        Lorem ipsum represents a long-held tradition for designers,
                                        typographers and the like. Some people hate it and argue for
                                        its demise, but others ignore the hate as they create awesome
                                        tools to help create filler text for everyone from bacon lovers
                                        to Charlie Sheen fans.
                                    </p>
                                    <form class="form-horizontal">
                                        <div class="input-group input-group-sm mb-0">
                                            <input class="form-control form-control-sm" placeholder="Response">
                                            <div class="input-group-append">
                                                <button type="submit" class="btn btn-danger">Send</button>
                                            </div>
                                        </div>
                                    </form>
                                </div>
                                <!-- /.post -->

                            </div>
                            <!-- /.tab-pane -->

                            <div class="tab-pane active" id="settings">
                                <form class="form-horizontal">
                                    <div class="form-group">
                                        <label for="name" class="col-sm-2 control-label">Name</label>
                                        <div class="col-sm-10">
                                            <input type="text" v-model="form.name" class="form-control" :class="{ 'is-invalid': form.errors.has('name') }" id="name" placeholder="Name">
                                            <has-error :form="form" field="name" ></has-error>
                                        </div>
                                    </div>
                                    <div class="form-group">
                                        <label for="email" class="col-sm-2 control-label">Email</label>
                                        <div class="col-sm-10">
                                            <input type="email" v-model="form.email" class="form-control" :class="{ 'is-invalid': form.errors.has('email') }" id="email" placeholder="Email">
                                            <has-error :form="form" field="email" ></has-error>
                                        </div>
                                    </div>
                                    
                                    <div class="form-group">
                                        <label for="bio" class="col-sm-2 control-label">Bio</label>
                                        <div class="col-sm-10">
                                            <textarea v-model="form.bio" class="form-control" id="bio" placeholder="Experience"></textarea>
                                        </div>
                                    </div>

                                    <div class="form-group">
                                        <label for="profilePhoto" class="col-sm-2 control-label">Profile Photo</label>
                                        <div class="col-sm-10">
                                            <input type="file" @change="updatePhoto"  id="profilePhoto" name="photo" placeholder="Password">
                                        </div>
                                    </div>


                                    <div class="form-group">
                                        <label for="passwprd" class="col-sm-2 control-label">Password</label>
                                        <div class="col-sm-10">
                                            <input type="password" v-model="form.password" class="form-control" 
                                            :class="{ 'is-invalid': form.errors.has('password') }" 
                                            id="password" placeholder="Password"
                                            autocomplete="new-password"
                                            >
                                            <has-error :form="form" field="password" ></has-error>
                                        </div>
                                    </div>
                                    
                                    <div class="form-group">
                                        <div class="col-sm-offset-2 col-sm-10">
                                            <button @click.prevent="updateInfo" type="submit" class="btn btn-danger">Save Changes</button>
                                        </div>
                                    </div>
                                </form>
                            </div>
                            <!-- /.tab-pane -->
                        </div>
                        <!-- /.tab-content -->
                    </div>
                    <!-- /.card-body -->
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {

        data(){
            return {

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
        mounted() {
        },

        methods:{

            getProfilePhoto(){
                //return "img/profile/"+this.form.photo;
                let prefix = (this.form.photo.match(/\//) ? '' : '/img/profile/');
                return prefix + this.form.photo;
            },

            updateInfo(){
                this.$Progress.start();
                this.form.put('api/profile')
                .then(() => {

                    swal.fire(
                        'Updated!',
                        'Your info has been updated.',
                        'success'
                    );

                    this.$Progress.finish();
                })
                .catch(() => {
                    this.$Progress.fail();
                })

            },
            updatePhoto(e){
                let file = e.target.files[0];
                let reader = new FileReader();
                if(file['size'] < 2111775){

                    reader.onloadend = (file) => {
                        this.form.photo = reader.result;
                    }
                    reader.readAsDataURL(file);
                }
                else{
                    swal.fire(
                        'error!',
                        'The file size is larger than 2 MB',
                        'error'
                    );
                }
            },


        },

        created() {
            axios.get('api/profile').then(({ data }) => (this.form.fill(data)));
        }
    }
</script>
