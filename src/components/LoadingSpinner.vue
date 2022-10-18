<template>
    <div class="bg-spinner d-flex flex-column justify-content-center align-items-center">
        <div class="lds-ring"><div></div><div></div><div></div><div></div></div>
        <span class="ms-2">Loading...</span>
    </div>
    
</template>

<script>
    export default {                  
        
    }
</script>

<style lang="scss" scoped>

.bg-spinner {
  height: 500px;
  width: auto;
  background-color: rgba($color: #C5C5C5, $alpha: 0.2);
}
.lds-ring {
    display: inline-block;
    position: relative;
    width: 80px;
    height: 80px;
    
  }
  .lds-ring div {
    box-sizing: border-box;
    display: block;
    position: absolute;
    width: 64px;
    height: 64px;
    margin: 8px;
    border: 8px solid #808080;
    border-radius: 50%;
    animation: lds-ring 1.2s cubic-bezier(0.5, 0, 0.5, 1) infinite;
    border-color: #808080 transparent transparent transparent;
    z-index: 9999;
  }
  .lds-ring div:nth-child(1) {
    animation-delay: -0.45s;
  }
  .lds-ring div:nth-child(2) {
    animation-delay: -0.3s;
  }
  .lds-ring div:nth-child(3) {
    animation-delay: -0.15s;
  }
  @keyframes lds-ring {
    0% {
      transform: rotate(0deg);
    }
    100% {
      transform: rotate(360deg);
    }
  }
</style>