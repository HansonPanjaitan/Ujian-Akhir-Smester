<template>   

<!-- DATA COVID GLOBAL -->
    <div class="pt-16 px-48 pb-20" style="background-color: aliceblue">
        <div class="text-3xl font-extrabold text-gray-500">Data Global
            <div class="flex flex-row justify-between pt-14">
                <div class="justify-center flex flex-col rounded-xl flex items-center font-bold 
                    bg-indigo-400 text-gray-100 h-40 text-3xl ml-10" style="width: 250px">
                    <span class="p-4">Terkonfirmasi</span>    
                    <span class="p-4">{{ confirmed | numberFormat}}</span>
                </div>
                <div class="justify-center flex flex-col rounded-xl flex items-center font-bold 
                    bg-red-400 text-gray-100 h-40 text-3xl" style="width: 250px">
                    <span class="p-4">Meninggal</span>    
                    <span class="p-4">{{ deaths | numberFormat}}</span>
                </div>
                <div class="justify-center flex flex-col rounded-xl flex items-center font-bold 
                    bg-green-400 text-gray-50 h-40 text-3xl mr-10" style="width: 250px">
                    <span class="p-4">Sembuh</span>    
                    <span class="p-4">{{ recovered | numberFormat }}</span>
                </div>
            </div>

<!-- DATA COVID NEGARA -->
            <div class="pt-24">
                <div class="text-3xl font-extrabold text-gray-500">Data Negara
                    <div class="flex flex-row justify-between pt-14">
                    </div>
                </div>                
            
                <table class="border-2 bg-gray-50 border-gray-200 w-full">
                    <thead>
                    <tr>
                        <th class="border-2 bg-gray-200 border-gray-300 text-black text-lg font-semibold 
                            text-left text-center p-3" scope="col">NO.</th>
                        <th class="border-2 bg-gray-200 border-gray-300 text-black text-lg font-semibold 
                            text-left text-center" scope="col">NEGARA</th>
                        <th class="border-2 bg-gray-200 border-gray-300 text-black text-lg font-semibold 
                            text-left text-center" scope="col">TERKONFIRMASI</th>
                        <th class="border-2 bg-gray-200 border-gray-300 text-black text-lg font-semibold 
                            text-left text-center" scope="col">MENINGGAL</th>
                        <th class="border-2 bg-gray-200 border-gray-300 text-black text-lg font-semibold 
                            text-left text-center" scope="col">SEMBUH</th>
                    </tr>    
                    </thead>
                    <tbody>
                        <tr v-for="(item, nomor) in data.Countries" :key="nomor">
                        <th class="border-2 border-gray-300 bg-gray-200 text-black text-lg font-semibold 
                            text-left text-center" scope="row">{{ nomor + 1 }}</th>
                        <td class="border-2 border-gray-300 text-gray-600 text-lg font-semibold 
                            text-left pl-4 p-2">{{ item.Country }}</td>
                        <td class="border-2 border-gray-300 text-gray-600 text-lg font-semibold 
                            text-center">{{ item.TotalConfirmed | numberFormat }}</td>
                        <td class="border-2 border-gray-300 text-gray-600 text-lg font-semibold 
                            text-center">{{ item.TotalDeaths | numberFormat }}</td>
                        <td class="border-2 border-gray-300 text-gray-600 text-lg font-semibold 
                            text-center">{{ item.TotalRecovered | numberFormat }}</td>
                        </tr> 
                    </tbody>       
                </table> 
            </div>
        </div>
    </div>        

</template>

<script>

export default {
    data() {
        return {
            countries: {},
            data: {},
            confirmed: 0,
            deaths: 0,
            recovered: 0,
            
        }
    },
    filters: {
        numberFormat(number) {
            return number.toLocaleString();
        }
    },
    methods: {
        getCountries(){
            axios.get('https://api.covid19api.com/countries')
                .then(response => {
                    this.countries = response.data;
                })

        },
        getSummaryData() {
            axios.get('https://api.covid19api.com/summary')
                .then(response => {
                    const data = response.data;
                    this.data = data;
                    this.confirmed = data.Global.TotalConfirmed;
                    this.deaths = data.Global.TotalDeaths;
                    this.recovered = data.Global.TotalRecovered;
                })
        }
    },
    mounted() {
        this.getCountries();
        this.getSummaryData()
    }
    
}
</script>

<style>
    
</style> 