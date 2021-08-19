<template>
  <div>
      <div id='boardlists' class="board-lists">
           <div v-for="(list,index) in tasklist" :key="index" :id='list.id' class="board-list">
                <div class="list-title">
                        {{list.title}}
                 </div>
                   <draggable :list="list.tasks" :animation="200" ghost-class="ghost-card" group="_task">
                        <div v-for="(task,i) in list.tasks" :key="i" :id='task.id' class="card" draggable="true"  :_task="task">
                              <div class="">
                                    {{task.title}}

                                  <!-- Modal -->
                                  <button  class="btn btn-outline-info btn-sm editbtn hide" data-toggle="modal" :data-target="'#Modal'+task.id+list.list"><i class="fas fa-pencil-alt" style="font-size: 14px;"></i></button>
                              </div>
                                <div class="modal fade" :id="'Modal'+task.id+list.list" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
                                <div class="modal-dialog modal-lg" role="document">
                                    <div class="modal-content pd10">
                                    <div class="modal-header">
                                        <h5 class="modal-title" id="exampleModalLabel">{{task.title}}</h5>
                                        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                                        <span aria-hidden="true">&times;</span>
                                        </button>
                                    </div>
                                    <div class="modal-body">
                                        <div class="row">
                                            <div class="col-lg-12">
                                                <div class="headertext">
                                                    <i class="fas fa-align-left"></i> Descriptions
                                                </div>
                                               
                                            </div>
                                            <div class="col-lg-12">
                                                 <div class="form-group">
                                                   
                                                    <textarea class="form-control" rows="3" id="comment" v-model="task.descriptions"></textarea>
                                                </div>
                                            </div>
                                        </div>
                                          <div class="row">
                                            <div class="col-lg-12">
                                                <div class="headertext">
                                                    <i class="fas fa-align-left"></i> Activity
                                                </div>
                                               
                                            </div>
                                            <div class="col-lg-12">
                                                 <div class="form-group">
                                                   
                                                    <textarea class="form-control" rows="3" id="comment" v-model="task.actions"></textarea>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                    <div class="modal-footer">
                                        <button type="button" class="btn btn-secondary btn-sm" data-dismiss="modal">Close</button>
                                        <!-- <button type="button" class="btn btn-primary">Save changes</button> -->
                                    </div>
                                    </div>
                                </div>
                                </div>
                        </div>
                      

                     </draggable>
                  <div class="addtextCard">
                      <input :id="'newTask'+index" type="text"   placeholder="add a card" class="form-control addcard" v-on:keyup.enter="addNewTask(index,$event)"/>
                  </div>
            </div>
      
             <div  class="board-list" v-show="tasklist.length<5">
                     <input  type="text"   placeholder="add a list ..." class="form-control addcard" v-on:keyup.enter="addNewlist($event)"/>
            </div>
            
      </div>
  </div>
</template>

<script>
import draggable from "vuedraggable";
export default {
    components:{
        draggable
    },
 data(){
     return{
       
        tasklist:[{
            "title":" To Do",
            id:"list1",
            list:1,
            tasks:[
                  {
                "title":"Go Hiking",
                "id":"task1",
                "descriptions":[],
                list:1
            },
            ]
        },{
            "title":"Doing",
               id:"list2",
               list:2,
            tasks:[
                     {
                "title":"Watch Movies",
                "id":"task1",
                "descriptions":[],
                list:1
            },
             {
                "title":"Watch new GOT episode",
                "id":"task2",
                "descriptions":[],
                 list:3
            },
            ]
        },
        {
            "title":"Done",
               id:"list3",
               list:3,
            tasks:[
                  {
                "title":"Pay Tax",
                "id":"task1",
                "descriptions":[],
                 list:2
            }
            ]
        }
        ],
        tasks:[
            {
                "title":"Go Hiking",
                "id":"task1",
                "descriptions":"",
                "actions":"",
                list:1
            },
             {
                "title":"Watch Movies",
                "id":"task4",
                "descriptions":"",
                "actions":"",
                list:1
            },
            {
                "title":"Watch new GOT episode",
                "id":"task2",
               "descriptions":"",
                "actions":"",
                 list:3
            },
            {
                "title":"Pay Tax",
                "id":"task3",
                 "descriptions":"",
                "actions":"",
                 list:2
            }
        ]
     }
 },
 computed: {
    // getList () {
    //     var vm = this
    //     return function (list) {
    //          return vm.tasks.filter(item => item.list == list)
    //     }
    // }
},
 methods:{
     addNewTask(index,event){
         let taskid =this.tasklist[index].tasks.length+1
         let newTask ={
                "title":event.target.value,
                 "descriptions":"",
                "actions":"",
                id:'task'+taskid,
                 list:index+1
            }
            this.tasklist[index].tasks.push(newTask);
            document.querySelector("#"+event.target.id).value="";

     },
     addNewlist(event){
         let newList ={
            "title":event.target.value,
            id:"list"+this.tasklist.length+1,
            tasks:[],
            list:this.tasklist.length+1
            }
            this.tasklist.push(newList);
             document.querySelector("#"+event.target.id).value="";
     },
     allowDrop(ev) {
    ev.preventDefault();  // default is not to allow drop
  },
//    dragStart(evt,item) {
//       evt.dataTransfer.dropEffect = 'move'
//       evt.dataTransfer.effectAllowed = 'move'
//       evt.dataTransfer.setData('itemID', item.id)
//   },
//   dropIt(evt,list,index) {
//         const itemID = evt.dataTransfer.getData('itemID');
//         let targetPrent =evt.currentTarget.id
//         let task =this.tasks.find(item => item.id == itemID);
//          let targetEl=document.getElementById(evt.target.id)
    
//       console.log(list)
//       task.list =list
//       console.log(index,targetPrent)
//   }
 }
}
</script>

<style>

</style>