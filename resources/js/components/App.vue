<template>
        <div class="app-component">
              <table class="table">
                  <thead>
                      <tr>
                          <th>ID</th>
                          <th>Task Title</th>
                          <th>Priority</th>
                          <th>Action</th>
                      </tr>
                  </thead>
                  <tbody>
                      <task v-for="task in tasks" :key='task.id' :task="task"></task>

                       <tr>
                           <td></td>
                         <td><input v-model="task.title" type="text" id="text" class="form-control"></td>
                         <td>
                             <select  v-model="task.priority" id="select" class="form-control">
                                 <option >Low</option>
                                 <option >Medium</option>
                                 <option >High</option>
                             </select>
                        </td>
                             <td>
                                 <button @click.prevent="store" type="button" class="btn btn-outline-primary">ADD</button>
                             </td>
                      </tr>
                
                  </tbody>
              </table>
        </div>
</template>

<script>
import Task from './Task.vue';
export default {
    data(){
        return{
            tasks:[
               
            ],
            message:'hello vue.js',
            task:{title:'',priority:''}
        }
    },

    methods:{

        readTasks(){

            axios.get('/api/tasks').then(({data})=>{
                data.forEach(task=>{
                    this.tasks.push(task)
                });
            });
        },

        store(){
           // console.log(this.task.title+' '+this.task.priority);
           //hadchi dyau
        //    axios.post('/api/tasks',{
        //        title:this.task.title,
        //        priority:this.task.priority
        //    }).catch(({errors})=>{
        //        console.log('Something went wrong')
        //    }).then(({data})=>{
        //        console.log(data);
        //    })


               axios.post('/api/tasks',this.task).then(save=>{
               this.tasks.push(save.data);
               
           });
        }
    },
    created(){
        this.readTasks();
    },
    components:{Task}
}
</script>
<style>

</style>