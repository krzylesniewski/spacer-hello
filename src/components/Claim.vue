<template>
    <div class="claimWrapper">
        <h1 class="claim">spacer</h1>
        <p class="subClaim">
             Rozpocznij swoją podróż przez naszą wspaniałą galaktykę,
             odkryj miejśca, o któych nigdy nie słyszałeś
        </p>
        <p class="subClaim">
            Wpisz cokolwiek związane z kosmosem
        </p>
    </div>
</template>
<script>
export default {
  name: 'Claim',
};
</script>
<style lang="scss" scoped>
    .claimWrapper{
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        color: #fff;
    }
    .claim{
        font-size: 50px;
        text-transform: uppercase;
        margin: 0;
        @media (min-width: 768px){
            font-size: 80px;
        }
    }
    .subClaim{
        font-size: 15px;
        margin: 20px 0 0 0;
        text-align: center;
        width: 80%;
        @media (min-width: 768px){
            font-size: 20px;
            width: 60%;
        }
    }
</style>

