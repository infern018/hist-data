<template>
  <span>
    Made with <i class="fa fa-heart pulse"></i> by <a href="https://github.com/infern018" target="_blank">infern018</a>
</span>
</template>

<script>
export default {

}
</script>

<style>
    
span{
  position: relative;
  top: 20px;
  padding-bottom: 10px !important;
  right: auto;
  transform: translateX(-50%) translateY(-50%);
  text-align: center;
  color: white;
}
  a{
    color: white;
    text-decoration: none;
  }
  .fa{
    color: #aa2a2a;
    margin: 0 3px;
    font-size: 14px;
    animation: pound .35s infinite alternate;
    -webkit-animation: pound .35s infinite alternate;
  }
</style>