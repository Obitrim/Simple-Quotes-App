<template>
    <div id="tracker">
        <h4> <span v-show="total_items === 0">NO</span> Quotes Added </h4>
        <div class="track">
            <div 
                class="track-inner" 
                :style="{ 'max-width' : (total_items / max) * 100 + '%' }"
                v-show="total_items > 0"
                >
                
                {{ total_items }} / {{ max }}
            </div>
        </div>
    </div>
</template>


<script>
    export default {

        data(){
            return {
                total_items: this.itemsAdded
            }
        },


        props:{
            itemsAdded: {
                type: Number,
                required: true
            },

            max: {
                type: Number,
                default: 20
            }
        },


        watch: {
            total_items: function(newValue){
                if(newValue > this.max){
                    alert("Slots full");
                }
            },

            itemsAdded(newSize){
                this.total_items = newSize;
            }
        }
    };
</script>


<style scoped>

    h4 {
        margin-top: 20px;
        font-size: .75rem;
        font-family: sans-serif;
        text-transform: uppercase;
        color: rgb(165, 161, 161);
    }

    #tracker {
        width: 100%;
    }

    .track {
        width: inherit !important;
        overflow: hidden;
        border-radius: 15px;
        background-color: rgb(235, 235, 235);
        box-shadow: inset 0 0 3px rgba(0, 0, 0, 0.25);
    }

    .track-inner {
        color: #fff;
        transition: 0.3s;
        text-align: center;
        background-color: #b90913 ;
        overflow-x: visible;
    }


    @media only screen and (max-width: 576px){
        .track-inner {
            font-size: 0.7rem;
        }
    }
</style>

