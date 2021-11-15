<template>
    <div class="row">
        <div class="container col">
                        <div class="form-group">
                            <input type="text" class="form-control" placeholder="Add Group" style="width: 30%;" v-on:keyup.enter="tambahGroup">
                          </div>
                          <div class="row mt-5">
                            <Room v-for="(item,index) in groups" v-bind:title="item" v-bind:key="index" v-bind:id="index" :players="users" v-on:addplayer="addplayer" v-on:deleteplayer="deleteplayer" v-on:deletegroup="deletegroup"></Room>
                        </div>
                    </div>
        <div class="col-3">
                        <div class="card text-white bg-dark" style="width: 18rem;float: right;overflow-y: hidden;">
                            <div class="card-header">
                              User Online
                            </div>
                            <ul class="list-group list-group-flush ">
                                <template v-if="users.length > 0">
                                    <li class="list-group-item text-white bg-dark" v-for="(item,index) in users" :key="index">
                                        {{ item.nama }}<span class="badge badge-success" style="float: right;">{{ item.status }}</span>
                                    </li>
                                </template>
                              
                                <li class="list-group-item text-white bg-dark" v-else>
                                    No Player Ready
                                </li>
                            </ul>
                          </div>
                    </div>
                    
    </div>
    
</template>

<script>
import Room from './Room.vue'

export default {
  name: 'Group',
  components: {
      Room
  },
  data: function () {
      return {
          users: [{
                    nama: "Hu Tao",
                    status: "online"
                },{
                    nama: "Raiden Shogun",
                    status: "online"
                },{
                    nama: "Eula",
                    status: "online"
                },{
                    nama: "Keqing",
                    status: "online"
                }],
                groups: ["Adeptus", "Knight of Favonius", "Tenryu Commission"]
      }
  },
 methods: {
                tambahGroup: function(event){
                    if(event.target.value == ""){
                        alert("Group name cannot be empty")
                    } else {
                        this.groups.push(event.target.value)
                        event.target.value = ""
                    }
                },
                deleteplayer: function(data){
                    this.users = this.users.filter(item => item.nama != data)
                },
                deletegroup: function(id, data){
                    this.groups.splice(id, 1)
                    if(data.length>0){
                        data.forEach(element => {
                            console.log(element)
                            this.users.push({nama: element, status: "online"})
                        });
                    }
                },
                addplayer: function(data){
                    this.users.push({nama: data, status: "online"})
                }
            },
}
</script>