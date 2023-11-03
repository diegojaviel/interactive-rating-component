<template>
  <div class="card-wrapper">
    <div class="card-content" v-if="!isSubmitted">
      <div class="star">
        <img src="../assets/images/icon-star.svg" alt="Star Img">
      </div>
      <h1>How did we do?</h1>
      <p>  Please let us know how we did with your support request. All feedback is appreciated to help us improve our offering!</p>
      <div class="ratings-wrap">
        <div v-for="(rating, index) in ratingNumbers" :key="index" class="rating" :class="{'selected-rating' : rating.selected}" @click="selectRating(index)">
          <span>{{rating.rating}}</span>
        </div>
      </div>
      <button @click="submitForm">Submit</button>
    </div>

    <div class="card-content thank-you" v-else>
      <img src="../assets/images/illustration-thank-you.svg" alt="">
      <div class="selection">
        <span>You selected {{ selectedRating.rating }} out of 5</span>
      </div>
      <h1>Thank you!</h1>
      <p>We appreciate you taking the time to give a rating. If you ever need more support, don’t hesitate to get in touch!</p>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

  const ratingNumbers = ref([
    {
      rating: 1,
      selected: false,
    },
    {
      rating: 2,
      selected: false,
    },
    {
      rating: 3,
      selected: false,
    },
    {
      rating: 4,
      selected: false,
    },
    {
      rating: 5,
      selected: false,
    },

  ])

  const selectedRating = ref(null);
  const isSubmitted = ref(null);

  function submitForm() {
    if(selectedRating.value){
      isSubmitted.value = true;
    }
  }

  function selectRating(index){
    ratingNumbers.value.forEach(rating => rating.selected = false)
    ratingNumbers.value[index].selected = true;
    selectedRating.value = ratingNumbers.value[index];
  }
</script>

<style scoped>
  .card-wrapper{
    display: grid;
    place-items: center;
    height: 100vh;
    background-color: var(--very-dark-blue);
    padding: 0 16px;
  }

  .card-content{
    background: var(--gradient, radial-gradient(98.96% 98.96% at 50% 0%, #232A34 0%, #181E27 100%));
    color: var(--white);
    max-width: 412px;
    width: 100%;
    padding: 32px;
    border-radius: 30px;
  }

  .star{
    display: grid;
    place-items: center;
    width: 48px;
    height: 48px;
    background-color: var(--dark-blue);
    border-radius: 50%;
    margin-bottom: 30px;
  }

  h1 {
    font-size: 28px;
    font-weight: 700;
    margin-bottom: 7px;
  }

  p{
    color: var(--light-grey);
    margin-bottom: 24px;
    line-height: 24px;
    font-size: 15px;
  }

  .ratings-wrap{
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
    gap: 22px;
  }

  .rating{
    display: grid;
    place-items: center;
    width: 51px;
    height: 51px;
    background-color: var(--dark-blue);
    color: var(--light-grey);
    border-radius: 50%;
    margin-bottom: 32px;
    cursor: pointer;
    transition: .5s ease all;
  }

  .selected-rating{
    background-color: var(--medium-grey);
    color: var(--white);
  }

  .rating:hover{
    background-color: var(--orange);
    color: var(--white);
  }

  button{
    padding: 12px;
    width: 100%;
    border-radius: 22px;
    background-color: var(--orange);
    color: var(--white);
    text-transform: uppercase;
    border: none;
    font-size: 15px;
    font-weight: 700; 
    letter-spacing: 2px;
    transition: .5s ease all;
    cursor: pointer;
  }
  
  button:hover{
    background-color: var(--white);
    color: var(--orange);
  }

  .thank-you{
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
  }

  .thank-you img{
    margin-bottom: 36px;
  }

  .selection{
    color: var(--orange);
    background-color: var(--dark-blue) ;
    padding: 4px 20px;
    border-radius: 22px;
    font-size: 15px;
    line-height: 24px;
    margin-bottom: 36px;
}

.thank-you p {
  margin-bottom: 0;
}
</style>