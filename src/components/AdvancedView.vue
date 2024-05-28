<template>
    <div class="statistics">
        <div class="statistics__heading">
            <h1>Advanced Statistics</h1>
            <p>  Track how your links are performing across the web with our 
            advanced statistics dashboard.</p>
        </div>
        <div class="statistics__boxes">
            <div v-for="(box,i) in boxes" :key="i" class="box">
                <div class="logo"><img :src="box.logo"/></div>
                <h4>{{ box.Name }}</h4>
                <p>{{ box.text }}</p>
            </div>
        </div>
    </div>
</template>

<script>
    import brandIcon from '../assets/images/icon-brand-recognition.svg';
    import customizable from '../assets/images/icon-fully-customizable.svg';
    import details from '../assets/images/icon-detailed-records.svg'
    export default{
    name:'AdvancedView',


     data(){
        return{
            boxes:[
                {
                    logo:brandIcon,
                    Name:'Brand Recognition',
                    text:'  Boost your brand recognition with each click. Generic links do not mean a thing. Branded links help instil confidence in your content.'
            },
            {
                    logo:customizable,
                    Name:'  Fully Customizable',
                    text:'    Gain insights into who is clicking your links. Knowing when and where people engage with your content helps inform better decisions.'
            },
            {
                    logo:details,
                    Name:'Detailed Records',
                    text: 'Improve brand awareness and content discoverability through customizable links, supercharging audience engagement.'
            }
        ]
        }
    }
}
</script>