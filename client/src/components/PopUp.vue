<template>
    <div>
        <button class="popup-open-button" @click="openPopup()">Yorum Yap</button>

        <div v-if="isPopupOpen" class="popup-overlay">
            <div class="popup-content">
                <h2 class="popup-title">Popup İçeriği</h2>
                <p class="popup-text">Merhaba, bu bir popup ekranıdır.</p>
                <button class="popup-close-button" @click="closePopup()">Kapat</button>
            </div>
        </div>
    </div>
</template>

<script>

import router from "../router";
import axios from "axios";

export default {
    data() {
        return {
            isPopupOpen: false
        };
    },
    methods: {
        openPopup() {
            this.isPopupOpen = true;
        },
        closePopup() {
            this.isPopupOpen = false;
        }
    }
};

</script>

<style>
.popup-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 4;
}


.popup-content {
    background-color: white;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.3);
    z-index: 4;
}

.popup-content h2 {
    margin-top: 0;
    z-index: 4;
}

.popup-content p {
    margin-bottom: 20px;
    z-index: 4;
}

.popup-content button {
    padding: 10px 20px;
    background-color: red;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    z-index: 4;
}

.popup-open-button{
    background-color: rgb(16, 214, 16);
    border-radius: 4px;
    color: white;
}

.popup-open-button:hover{
    background-color: rgba(0, 128, 0, 0.671);
}

.popup-close-button:hover{
    background-color: rgb(212, 22, 22);
}
</style>