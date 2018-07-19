<template>
  <div class="outerWrapper">
    <div class="innerWrapper">
      <div class="photo">
          <img src="https://images.pexels.com/photos/264635/pexels-photo-264635.jpeg?auto=compress&cs=tinysrgb&h=650&w=940" alt="" srcset="">
      </div>
      <div class="description">
        <h2 class="title">Lorem ipsum</h2>
        <p class="description">
            Lorem ipsum dolor sit amet consectetur, adipisicing elit. 
            Suscipit, in laudantium quae, temporibus deserunt obcaecati labore
             minima optio est assumenda error asperiores necessitatibus odit, alias
             vel pariatur ex rerum tenetur.
        </p>
      </div>
    </div>
    <div class="close" @click="$emit('closeModal')"></div>
  </div>
</template>

<script>
export default {
  name: 'Modal',
};
</script>

<style lang="scss" scoped>
  .outerWrapper {
     max-width: 100%;
     height: 100%;
     position: fixed;
     top: 0;
     left: 0;
     background-color: white;

     @media (min-width: 1024px) {
         max-width: 70%;
         height: 60%;
         left: 0;
         right: 0;
         top: 0;
         bottom: 0;
         margin: auto;
         box-shadow: 0 30px 30px -10px rgba(0,0,0, .3);
     }
  }
  .innerWrapper {
    display: flex;
    height: 100%;
    padding: 50px;
    justify-content: center;
    align-items: center;
    flex-direction: column;

    @media (min-width: 1024px) {
      flex-direction: row;
      .photo {
          width: 50%;
          margin-right: 20px;
      }
    }
  }
  .photo {
    min-width: 50%;
    height: 80%;
  }
  img {
      width: 100%;
  }
  .close {
      position: absolute;
      width: 30px;
      height: 30px;
      padding: 30px;
      right: 0;
      top: 0;
      cursor: pointer; 

      &::before,
      &::after {
          position: absolute;
          content: '';
          top: 20px;
          right: 20px;
          width: 20px;
          height: 2px;
          background: black;
          display: block;

      }
      &::before {
          transform: rotate(45deg);
      }
      &::after {
          transform: rotate(-45deg);
      }
  }
</style>
