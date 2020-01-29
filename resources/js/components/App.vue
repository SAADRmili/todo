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
                         <td><input type="text" id="text" class="form-control"></td>
                         <td>
                             <select  id="select" class="form-control">
                                 <option >Low</option>
                                 <option >Medium</option>
                                 <option >High</option>
                             </select>
                        </td>
                             <td>
                                 <button type="button" class="btn btn-outline-primary">ADD</button>
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
            message:'hello vue.js'
        }
    },

    methods:{

        readTasks(){

            axios.get('/api/tasks').then(({data})=>{
                data.forEach(task=>{
                    this.tasks.push(task)
                });
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