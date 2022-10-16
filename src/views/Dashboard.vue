<template>
    <div class="dashboard p-4">
        <div>
            <LoadingSpinner/>
        </div>
        <h1 class="text-center m-3">Dashboard Demo</h1>

        <label class="mb-3" for="search">Search</label>
        <input type="text" id="search" v-model="searchValue" class="form-control mb-3" placeholder="Searching: " />

        <!-- <div class="mb-3">
            <p>You searched for: {{ searchValue }}</p>
        </div> -->

        <table class="table">
            <thead>
                <tr>
                    <th scope="col">Index</th>
                    <th scope="col">Name</th>
                    <th scope="col">Fee</th>
                    <th scope="col">Processing Fee</th>
                    <th scope="col">Transportation Fee</th>
                    <th scope="col">Payment Status</th>
                    <th scope="col">Total Fee</th>
                    <th>Action</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(staff, index) in staffList">
                    <!-- use index if want to print it out -->
                    <td>{{index + 1}}</td> <!-- +1 bcs index started from 0 -->
                    <td>{{staff.user.name}}</td> <!-- print out name -->
                    <td>RM {{staff.amount}}</td> <!-- print out amount -->
                    <td>RM {{staff.processing_fee}}</td> <!-- print out fee -->
                    <td>RM {{staff.transportation_fee}}</td> <!-- print out fee -->
                    <td><span id="badge" class="badge bg-secondary ms-3"
                            :class="staff.status == 'pending' ? 'bg-danger' : 'bg-success'">{{staff.status}}</span></td>
                    <!-- condition to make the badge change colour, ( element == "true?" ? true condition : false condition ) -->
                    <td>RM {{staff.amount + staff.processing_fee + staff.transportation_fee}} </td>
                    <!-- use case basis: calculate total in the most basic way -->
                    <td><button @click="handleClickButton(staff)" :disabled="staff.status != 'pending'" type="button"
                            class="btn border-dark" :class="staff.status == 'pending' ? 'text-danger' : 'text-success'">
                            {{ staff.status == 'pending' ? 'sila bayar' : 'selesai'}}

                            <!-- v-if="staff.status == 'pending'" : to show only pending status using v-if -->
                        </button></td>
                </tr>
            </tbody>
        </table>

    </div>
</template>

<script>
import { onMounted } from 'vue';
import LoadingSpinner from "@/components/LoadingSpinner";

export default {
    name: 'dashboard',
    components: { LoadingSpinner },
    data: function () {
        return {
            staffs: [],
            isActive: false,
            hasError: false,
            name: '',
            searchValue: '',
            timeout: 0,
            isLoading: false

        }
    },

    watch: {
        // searchValue: {
        //     handler() {
        //         console.log(this.searchValue);
        //     }
        // }
    },


    methods: {
        handleClickButton(str) {
            console.log(str);
        },
        capFirst(string) {
            return string.charAt(0).toUpperCase() + string.slice(1);
        },
        getRandomInt(min, max) {
            return Math.floor(Math.random() * (max - min)) + min;
        },
        generateName(i) {
            var first_name = ["hassan", "ali", "sarah", "siti", "karim", "zul", "zahir", "hassan", "ali", "sarah", "siti", "karim", "zul", "zahir", "hassan", "ali", "sarah", "siti", "karim", "zul", "zahir", "hassan", "ali", "sarah", "siti", "karim", "zul", "zahir"];

            var last_name = ["senah", "abu", "halim", "abdul", "karim", "zul", "zahir", "senah", "abu", "halim", "abdul", "karim", "zul", "zahir", "hassan", "ali", "sarah", "siti", "karim", "zul", "zahir", "hassan", "ali", "sarah", "siti", "karim", "zul", "zahir"];

            var name = this.capFirst(first_name[this.getRandomInt(0, i + 1)]) + ' ' + this.capFirst(last_name[this.getRandomInt(0, i + 1)]);

            return name
        },

        randomArray() {
            let arrays = []
            for (let i = 0; i < 30; i++) {
                arrays.push({
                    id: (Math.random() + 1).toString(36).substring(7),
                    user: {
                        id: (Math.random() + 1).toString(36).substring(7),
                        name: this.generateName(i)
                    },
                    amount: Math.floor(Math.random() * 10),
                    transportation_fee: Math.floor(Math.random() * 3),
                    processing_fee: Math.floor(Math.random() * 1),
                    status: i % 2 == 0 ? 'pending' : 'paid'
                })
            }
            return arrays
        },

        clear() {
            clearTimeout(this.timeout) // to clear time out. it will keep counting until reach certain number and clear
        }
    },

    computed: {
        // choose method for use-case basis
        // totalSum() {
        //     return this.staffs.reduce((totalSum, currentVal) => totalSum + currentVal.amount, 0); // 0 is initial value
        // },

        staffList() {
            if (this.searchValue.trim().length > 0) {
                if (this.timeout) {
                    this.clear()
                }

                this.timeout = setTimeout(() => {
                    let newData = this.staffs
                    console.log(this.timeout)
                    this.staffs = newData.filter((staff) => staff.user.name.toLowerCase().includes
                        (this.searchValue.trim().toLowerCase()))
                }, 500)
                
            }
            return this.staffs
        }
    },

    mounted() {
        this.staffs = this.randomArray(); //simpan loaded data dekat sini

        // console.log(this.staffs);
    }

}
</script>





