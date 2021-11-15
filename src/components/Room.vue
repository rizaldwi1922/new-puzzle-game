<template>
    <div>
            <div class="card m-2" style="width: 18rem;">
                                <div class="card-header">
                                  {{ title }}
                                  <a href="#" v-on:click.prevent="deletelist" style="float: right" >
                                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="red" class="bi bi-trash" viewBox="0 0 16 16">
                                        <path d="M5.5 5.5A.5.5 0 0 1 6 6v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5zm2.5 0a.5.5 0 0 1 .5.5v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5zm3 .5a.5.5 0 0 0-1 0v6a.5.5 0 0 0 1 0V6z"/>
                                        <path fill-rule="evenodd" d="M14.5 3a1 1 0 0 1-1 1H13v9a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V4h-.5a1 1 0 0 1-1-1V2a1 1 0 0 1 1-1H6a1 1 0 0 1 1-1h2a1 1 0 0 1 1 1h3.5a1 1 0 0 1 1 1v1zM4.118 4 4 4.059V13a1 1 0 0 0 1 1h6a1 1 0 0 0 1-1V4.059L11.882 4H4.118zM2.5 3V2h11v1h-11z"/>
                                    </svg>
                                  </a>
                                  <a href="#" v-on:click.prevent="showmodal" style="float: right;"><span class="fa fa-plus mr-3"></span> </a>
                                </div>
                                <ul class="list-group list-group-flush">
                                    <template v-if="users.length > 0">
                                        <li class="list-group-item" v-for="(user, index) in users" :key="index">{{ user }}
                                            <a href="#" v-on:click.prevent="deleteplayers(index)" style="float: right" >
                                            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="red" class="bi bi-trash" viewBox="0 0 16 16">
                                                <path d="M5.5 5.5A.5.5 0 0 1 6 6v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5zm2.5 0a.5.5 0 0 1 .5.5v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5zm3 .5a.5.5 0 0 0-1 0v6a.5.5 0 0 0 1 0V6z"/>
                                                <path fill-rule="evenodd" d="M14.5 3a1 1 0 0 1-1 1H13v9a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V4h-.5a1 1 0 0 1-1-1V2a1 1 0 0 1 1-1H6a1 1 0 0 1 1-1h2a1 1 0 0 1 1 1h3.5a1 1 0 0 1 1 1v1zM4.118 4 4 4.059V13a1 1 0 0 0 1 1h6a1 1 0 0 0 1-1V4.059L11.882 4H4.118zM2.5 3V2h11v1h-11z"/>
                                            </svg>
                                        </a>    
                                        </li>
                                        
                                    </template>
                                    <li class="list-group-item" v-else>No Player</li>
                                </ul>
                        </div>
                        <div class="modal fade" :id="'add-user' + id" tabindex="-1" role="dialog" aria-hidden="true">
                            <div class="modal-dialog modal-dialog-centered" role="document">
                            <div class="modal-content">
                                <div class="modal-header">
                                <h5 class="modal-title" id="exampleModalLongTitle">Add player to {{ title }}</h5>
                                <button type="button" class="close" v-on:click="closeModal">
                                    <span aria-hidden="true">&times;</span>
                                </button>
                                </div>
                                <div class="modal-body">
                                    <ul class="list-group">
                                        <template v-if="players.length > 0">
                                            <li class="list-group-item" v-for="(item, index) in players" :key="index">{{ item.nama }} <a href="#" v-on:click.prevent="addplayer(item.nama)" style="float: right;"><span class="fa fa-plus mr-3"></span> </a>  </li>
                                        </template>
                                        <li class="list-group-item" v-else>No Player</li>
                                        
                                    </ul>
                                </div>
                            </div>
                            </div>
                        </div>
                        </div>
</template>
<script>
export default {
  name: 'Room',
  props:{
      title: String,
      players: Array,
      id: Number
  },
  data: function () {
      return {
          users: [],
      }
  },
  methods: {
                showmodal: function(){
                    var modal = document.getElementById("add-user" + this.id);
                    modal.classList.add("show");
                    modal.style.display = "block";
                },
                closeModal: function() {
                    var modal = document.getElementById("add-user" + this.id);
                    modal.classList.remove("show");
                    modal.style.display = "none"; 
                },
                addplayer: function(data) {
                    this.users.push(data)
                    this.$emit('deleteplayer', data)
                    console.log(this.title)
                },
                deletelist: function(){
                    this.$emit('deletegroup', this.id, this.users)
                    this.users = []
                },
                deleteplayers: function(id){
                    var nama = this.users[id]
                    this.$emit("addplayer", nama)
                    this.users.splice(id, 1)
                }
            }
}
</script>