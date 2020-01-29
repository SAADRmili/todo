<template>
        <div class="app-component">
              <table class="table">
                  <thead>
                      <tr>
                          <th>Task Title</th>
                          <th>Priority</th>
                          <th>Action</th>
                      </tr>
                  </thead>
                  <tbody>
                      <task v-for="task in tasks" :key='task.id' :task="task"></task>

                       <tr>
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
                {
                    id:1,
                    title:'Task1',
                    priority:'low'
                },
                {
                    id:2,
                    title:'Task2',
                    priority:'low'
                },
                {
                    id:3,
                    title:'Task3',
                    priority:'low'
                },
            ],
            message:'hello vue.js'
        }
    },
    components:{Task}
}
</script>
<style>

</style>