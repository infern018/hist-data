<template>
  
  <h2 class="details-head">DETAILS</h2>
  <div class="courses-container">
	<div class="course">
		<div class="course-preview">
			<h6>Code</h6>
			<h2>{{ hist.Code }}</h2>
		</div>
		<div class="course-info">
			<h6>Age:</h6>
            <h2>{{ hist.Age }}</h2>

            <h6>Sex:</h6>
            <h2>{{ hist.Sex }}</h2>

            <h6>Body Weight(g):</h6>
            <h2>{{ hist.BodyWeight }}</h2>

            <h6>Parts:</h6>
            <h2>{{ hist.Parts }}</h2>

            <h6>Staining:</h6>
            <h2>{{ hist.Staining }}</h2>

            <h6>Plane of Sectioning:</h6>
            <h2>{{ hist.PlaneOfSectioning }}</h2>

		</div>
	</div>
</div>
<Footer />
</template>

<script>
import Footer from '../components/Footer'
import { ref } from 'vue'
export default {
    props:['id'],
    components:{Footer},
    setup(props){
        const hist = ref(null)

        fetch('https://histdataapi.herokuapp.com/posts/'+props.id)
        .then(res => res.json())
        .then(data => {
            hist.value = data
            console.log(hist.value[0])

            for(var pr in hist.value)
            {
                if(hist.value[pr] == '')
                {
                    hist.value[pr] = '---'
                }
            }

			if(hist.value.Sex=='m'){
				hist.value.Sex='male';
			} else if(hist.value.Sex=='f'){
				hist.value.Sex='female'
			}

        })

    

        return {hist}
    }
}
</script>

<style>

@import url('https://fonts.googleapis.com/css?family=Muli&display=swap');

body {
	font-family: 'Muli', sans-serif!important;
	display: flex;
	align-items: center;
	justify-content: center;
	flex-direction: column;
	margin: 0;
}

.details-head{
    color: white;
}


.course {
	background-color: #fff;
	border-radius: 10px;
	box-shadow: 0 10px 10px rgba(0, 0, 0, 0.2);
	display: flex;
	max-width: 100%;
	margin: 20px;
	overflow: hidden;
	width: 700px;
    text-align: left;
}

.course h6 {
	opacity: 0.6;
	margin: 0;
	letter-spacing: 1px;
	text-transform: uppercase;
}

.course h2 {
	letter-spacing: 1px;
	margin: 10px 0;
}

.course-preview {
	background-color: #272e66;
	color: #fff;
	padding: 30px;
	max-width: 350px;
}

.course-info {
	padding: 30px;
	position: relative;
	width: 100%;
}


</style>