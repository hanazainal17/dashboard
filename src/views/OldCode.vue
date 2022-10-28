<template>
    <div>

    </div>
</template>

<script>
export default {
    computed: {
        // if (this.searchValue.trim().length > 0) {
        //     if (this.timeout) {
        //         this.clear()    
        //         this.isLoading = true
        //     }

        //     this.timeout = setTimeout(() => {
        //         let newData = this.staffs
        //         console.log(this.timeout)
        //         this.staffs = newData.filter((staff) =>
        //             staff.user.name
        //                 .toLowerCase()
        //                 .includes
        //                 (this.searchValue.trim().toLowerCase()))
        //                 this.isLoading = false
        //     }, 500)

        //     if (arr.length > 0) {
        //         let data = this.staffs
        //         newArr = data.filter((staff) =>
        //             staff.user.name
        //                 .toLowerCase()
        //                 .includes
        //                 (this.searchValue.trim().toLowerCase()))
        //     }   
        // }
        // //return this.randomArray()
        // return this.staffs
        staffList() {
            let listArr = this.randomArray()

            //trigger search and timeout
            if (this.searchValue.trim().length > 0) {
                    this.isLoading = true
            }

            const filterArray = listArr.filter((staff) =>
                staff.user.name
                    .toLowerCase()
                    .includes
                    (this.searchValue.trim().toLowerCase()))



            if (this.filterArray > 0) {
                listArr = filterArray
            }
            return listArr
        }
    }
}
</script>

<style lang="scss" scoped>

</style>