<template>
       
                      <tr>
                          <td>{{ task.id}}</td>
                          <td scope="row">{{ task.title}}</td>
                          <td>{{ task.priority}}</td>
                          <td>
                              <button type="button" class="btn btn-danger">Remove</button>
                          </td>
                      </tr>
                    
                
       
</template>

<script>
export default {
    props:['task'],
    data(){
        return{
            
        }
    }
}
</script>
<style>

</style>