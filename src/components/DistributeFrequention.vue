<template>
    <div>
        <input type="text" placeholder="data" id="data" v-model="data"/>
        <button id="generate" @click="onGenerate">Generate</button><br>
        <center>
            <table v-show="values.length>0" id="table">
                <thead>
                    <tr>
                        <th>No.</th>
                        <th>Nilai</th>
                        <th>Batas Kelas</th>
                        <th>Frequensi</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(item,i) in values" :key="i">
                        <td>{{ i+1 }}</td>
                        <td>{{ item.nilai }}</td>
                        <td>{{ item.bataskelas }}</td>
                        <td>{{ item.freq }}</td>
                    </tr>
                </tbody>
                <tfoot v-show="total>0">
                    <tr>
                        <td colspan="3">Jumlah</td>
                        <td>{{ total }}</td>
                    </tr>
                </tfoot>
            </table>
        </center>
    </div>
</template>
<script>
export default{
    data(){
        return{
            data: '',
            values:[],
            total:0
        }
    },
    mounted(){
        
    },
    methods:{
        max(data){
            if (toString.call(data) !== "[object Array]")  
                return false
            return Math.max.apply(null, data)
        },
        min(data){
            if (toString.call(data) !== "[object Array]")  
                return false
            return Math.min.apply(null, data)
        },
        log(data){
            return Math.log(data) / Math.log(10)
        },
        onGenerate(){
            let valueHolder = this.data.split(' ')
            valueHolder = valueHolder.filter(data=> data!='').map(data=>parseFloat(data))
            // let lolos = 0
            // valueHolder.forEach(val=>{
            //     if(val<49||val>54){lolos++}
            // })
            // console.log(this.max(valueHolder))
            
            let j = this.max(valueHolder) - this.min(valueHolder)
            let bk = Math.ceil(1 + (3.3*this.log(valueHolder.length)))
            let pk = Math.ceil(j/bk)

            let startVal = this.min(valueHolder);
            this.values = []
            this.total = 0
            for(let i = 0; i < bk; i++){
                let nextVal = startVal + pk-1
                let freqCount = 0
                valueHolder.forEach(val=>{
                    if(val>=(startVal-0.4)&&val<=(nextVal+0.5)){freqCount++}
                })
                this.values.push({
                    nilai:startVal+' - '+nextVal,
                    bataskelas:(startVal-0.5)+' - '+(nextVal+0.5),
                    freq:freqCount
                })
                this.total += freqCount
                startVal = nextVal+1
            }
            // console.log(this.values)
            console.log({data:{
                terkecil:this.min(valueHolder),
                terbesar: this.max(valueHolder),
                jangkauan:j,
                banyak_kelas:bk,
                panjang_kelas:pk
            }})
        }
    }
}
</script>

<style>
#data{
    width:400px;
    padding:10px;
    border:1px solid #1ac0c6;
}
#data:focus{
    outline:1px solid #fb7756;
    border:1px solid transparent;
}
#generate{
    padding:11px;
    margin-left:5px;
    background-color:#1ac0c6;
    border:none;
    color:white;
}
#generate:focus{
    outline:none;
}
#table{
    width:700px;
    border-collapse:collapse;
    border:1px solid black;
    margin-top:20px;
}
#table, tr, td, th{
    border:1px solid black
}
 th, td{
    padding:10px;
}
#table th{
    background:#dee0e6
}
</style>