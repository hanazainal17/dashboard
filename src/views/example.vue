<template>
    <div>
        <div class="col">
            <div class="row">
                <div class="card m-3" style="width: 30rem;">
                    <div class="card-body">
                        <h5 class="card-title">User</h5>
                        <div v-for="(staff, index) in staffs">
        
                            <p class="card-text"> {{ staff.id }} : RM {{ staff.amount }}
                                <span id="badge" class="badge bg-secondary ms-3" :class="statusColor">
                                {{staff.status}}
                                </span>
                                <!-- :class="{ 'completed' : staff.status == 'text-bg-success', 'pending' : staff.status == 'text-bg-warning' }" -->
                            </p>
                            
                        </div>
                    </div>
                </div>
        
                <div class="card m-3" style="width: 18rem;">
                    <div class="card-body">
                        <p class="card-text"> Total: RM {{ totalSum }}</p>
                    </div>
                </div>
        
            </div>
        
        </div>
    </div>
</template>

<script>
    export default {
        
    }
</script>

<style lang="scss" scoped>

</style>