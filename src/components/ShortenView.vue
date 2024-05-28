<template>
    <div class="shorten">
        <div class="shorten__input">
            <input @input="checkError" placeholder="Shorten a link here..." v-model="inputvalue" :class="{errorClass: error}" ref="reff"> 
            <button @click="fetchValidUrl">Shorten It</button>
            <p v-if="error">{{ errormessage }}</p>
        </div>
        <div class="shorten__links">
            <div  v-for="(link,i) in links" :key="i" class="flex">
                <h5>{{ link.longurl }}</h5>
                <div>
                    <a :href="link.shorturl">{{ link.shorturl }}</a>
                <button @click="copyLink(i)">{{ link.copyState }}</button>
                </div>
                
            </div>
        </div>
    </div>
</template>

<script>


    export default{
        name:'ShortenView',
        data(){
            return{
                links:[],
                inputvalue:'',
                error:false,
               errormessage:''
            }
        },

        props:['reff'],

        mounted(){
            this.getLink()        
        },


        methods:{

            getLink(){
                const urls = JSON.parse(sessionStorage.getItem('urls')) ||[]
                this.links=urls
            },

            checkError(){
                this.error=false
                    this.errormessage=''
            },

            fetchValidUrl(){
                const url = this.inputvalue

                if(url===''){
                    this.error=true
                    this.errormessage='input field cannot be empty'
                     return false 
                }

                try{
                    const newlink = new URL(url)

                    console.log(newlink)

                    if(newlink.protocol === 'https:'|| newlink.protocol === 'http:'){
                        this.error=false
                        this.errormessage=''
                        this.postLink(url)
                        return true

                    }

                    else{
                        this.error=true
                    this.errormessage='Please input a valid http link'
                        return false
                    }
                }

                catch(error){
                    console.log(error)

                    this.error=true
                    this.errormessage='Please input a valid http link'
                        return false    
                }
            },

            async postLink(url){
               
                const options ={

                    method: 'POST',
                    headers: {
                        accept: 'application/json',
                        'content-type': 'application/json',
                        'x-api-key': '9f7207c0-1ae8-11ef-8887-6382da94c80e'
                    },
                    body: 
                        JSON.stringify({"destinations":[{"url":url,"country":null,"os":null}]})
                    ,

                    
                }


               try{
                const res = await fetch('https://api.shorten.rest/aliases?aliasName=link/@rnd', options)

                    const data = await res.json()

                    const newlink = data.shortUrl

                    let newlinks =[ 
                                        {
                    longurl:url,
                    shorturl: newlink,
                    copyState:'copy'
                    
                    }, 
                    ...this.links
                ]
                sessionStorage.setItem('urls', JSON.stringify(newlinks))
                this.getLink()
                
                this.inputvalue=''
                }
            
            catch(err){
                    console.log(err.message)
            }
            },

            copyLink(index){

                navigator.clipboard.writeText(this.links[index].shorturl).then(() => 
                {
                   this.links[index].copyState ='copied'
                   setTimeout(()=>{
                    this.links[index].copyState ='copy'
                   },1000)
                },  () => {
                    this.links[index].copyState='try again'

                    setTimeout(()=>{
                    this.links[index].copyState ='copy'
                   },1000)
                    });

            }
        }

    }
</script>