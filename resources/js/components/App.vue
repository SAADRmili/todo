<template>
        <div class="app-component">
             <loading :active.sync="isLoading" ></loading>
        
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
                      <task v-for="task in tasks" :key='task.id' :task="task" @delete='remove'></task>

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
  // Import component
    import Loading from 'vue-loading-overlay';
    // Import stylesheet
    import 'vue-loading-overlay/dist/vue-loading.css';
export default {
    data(){
        return{
            tasks:[
               
            ],
            message:'hello vue.js',
            task:{title:'',priority:''},
            isLoading: false,
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
            if(this.checkInput())
            {
                this.isLoading=true;
                     axios.post('/api/tasks',this.task).then(save=>{
                     this.tasks.push(save.data);
                this.task.title='';
                this.task.priority='';
                this.isLoading=false;
                });
            }
              
        },
        checkInput(){
            if(this.task.title && this.task.priority) return true;
        },
        remove(id){
               this.isLoading = true;
                // simulate AJAX
             
            axios.delete(`/api/tasks/${id}`).then(()=>{
                let index = this.tasks.findIndex(task=>task.id === id);
                this.tasks.splice(index,1);
                this.isLoading=false
            });
        }
    },
    created(){
        this.readTasks();
    },
    components:{Task,Loading}
}
</script>
<style>

</style>