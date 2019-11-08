<template>
    <div class="wrapper contact-page">
        <div class="page-header page-header-small">
            <parallax class="page-header-image"
                 style="background-image: url('img/bg45.jpg')">
            </parallax>
        </div>

        <div class="main">
            <div class="contact-content">
                <div class="container">
                    <div class="row">
                        <div class="col-md-5 ml-auto mr-auto">
                            <h2 class="title">Send us a message</h2>
                            <p class="description">You can contact us with anything related to our Products. We'll get
                                in touch with you as soon as possible.
                                <br>
                                <br>
                            </p>
                            <form role="form" @submit.prevent="submitData()">
                                <label>Your name</label>
                                <div class="input-group mb-3">
                                <div class="input-group-prepend">
                                    <span class="input-group-text"><i class="now-ui-icons users_circle-08"></i></span>
                                </div>
                                <input type="text" class="form-control" v-model="form.name" placeholder="Your Name Here..." aria-label="Name" aria-describedby="basic-addon1" required>
                        </div>
                                <label>Email address</label>
                                <div class="input-group mb-3">
                                    <div class="input-group-prepend">
                                        <span class="input-group-text"><i class="now-ui-icons users_circle-08"></i></span>
                                    </div>
                                    <input type="email" class="form-control" v-model="form.email" placeholder="Email address Here..." aria-label="Email" aria-describedby="basic-addon1" required>
                                </div>

                                <label>Subject</label>
                                <div class="input-group mb-3">
                                    <div class="input-group-prepend">
                                        <span class="input-group-text"><i class="now-ui-icons tech_mobile"></i></span>
                                    </div>
                                    <input type="text" class="form-control" v-model="form.subject" placeholder="Subject Here..." aria-label="Subject" aria-describedby="basic-addon1" required>
                                </div>

                                <label>Purpose</label>
                                <div class="input-group mb-3">
                                    <div class="input-group-prepend">
                                        <span class="input-group-text"><i class="now-ui-icons emoticons_satisfied"></i></span>
                                    </div>
                                    <input type="text" class="form-control" v-model="form.purpose" placeholder="Purpose Here..." aria-label="Purpose" aria-describedby="basic-addon1" required>
                                </div>
                                <label>Your Message</label>
                                <div class="input-group mb-3">
                                     <textarea name="message" class="form-control" rows="6" v-model="form.message" required></textarea>
                                </div>
                                <div class="submit text-center">
                                    <button type="submit" class="btn btn-round btn-primary">Contact Us</button>
                                </div>
                            </form>
                        </div>
                        <div class="col-md-5 ml-auto mr-auto">
                            <info-section type="primary"
                                          class="mt-5"
                                          icon="now-ui-icons location_pin">
                                <h4 class="info-title">Find us at the office</h4>
                                <p> Bld Mihail Kogalniceanu, nr. 8,
                                    <br> 7652 Bucharest,
                                    <br> Romania
                                </p>
                            </info-section>

                            <info-section type="primary"
                                          icon="now-ui-icons tech_mobile">
                                <h4 class="info-title">Give us a ring</h4>
                                <p> Michael Jordan
                                    <br> +40 762 321 762
                                    <br> Mon - Fri, 8:00-22:00
                                </p>
                            </info-section>

                            <info-section type="primary"
                                          icon="business_briefcase-24 now-ui-icons">
                                <h4 class="info-title">Legal Information</h4>
                                <p> Creative Tim Ltd.
                                    <br> VAT · EN2341241
                                    <br> IBAN · EN8732ENGB2300099123
                                    <br> Bank · Great Britain Bank
                                </p>
                            </info-section>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <gmap-map
                id="map"
                class="big-map"
                :center="center"
                :zoom="13"
                :options="options"
                map-type-id="terrain">
            <gmap-marker :position="center">
            </gmap-marker>
        </gmap-map>
    </div>
</template>
<script>
  import { Button, InfoSection, FormGroupInput } from '@/components';
  import {API_KEY} from '@/constants'
  import Vue from 'vue'
  import * as VueGoogleMaps from 'vue2-google-maps'
  const axios = require('axios');
  Vue.use(VueGoogleMaps, {
    load: {
      key: API_KEY
    }
  });
  export default {
    name: 'contact-us',
    bodyClass: 'contact-page',
    components: {
      InfoSection,
      [Button.name]: Button,
      [FormGroupInput.name]: FormGroupInput,
    },
    data() {
      return {
        form: {
          name: '',
          email: '',
          subject: '',
          purpose: '',
          message: '',
        },
        center: {
          lat: 40.748817,
          lng: -73.985428
        },
        options: {
          styles: [{
            "featureType": "water",
            "elementType": "geometry",
            "stylers": [{
              "color": "#e9e9e9"
            }, {
              "lightness": 17
            }]
          }, {
            "featureType": "landscape",
            "elementType": "geometry",
            "stylers": [{
              "color": "#f5f5f5"
            }, {
              "lightness": 20
            }]
          }, {
            "featureType": "road.highway",
            "elementType": "geometry.fill",
            "stylers": [{
              "color": "#ffffff"
            }, {
              "lightness": 17
            }]
          }, {
            "featureType": "road.highway",
            "elementType": "geometry.stroke",
            "stylers": [{
              "color": "#ffffff"
            }, {
              "lightness": 29
            }, {
              "weight": 0.2
            }]
          }, {
            "featureType": "road.arterial",
            "elementType": "geometry",
            "stylers": [{
              "color": "#ffffff"
            }, {
              "lightness": 18
            }]
          }, {
            "featureType": "road.local",
            "elementType": "geometry",
            "stylers": [{
              "color": "#ffffff"
            }, {
              "lightness": 16
            }]
          }, {
            "featureType": "poi",
            "elementType": "geometry",
            "stylers": [{
              "color": "#f5f5f5"
            }, {
              "lightness": 21
            }]
          }, {
            "featureType": "poi.park",
            "elementType": "geometry",
            "stylers": [{
              "color": "#dedede"
            }, {
              "lightness": 21
            }]
          }, {
            "elementType": "labels.text.stroke",
            "stylers": [{
              "visibility": "on"
            }, {
              "color": "#ffffff"
            }, {
              "lightness": 16
            }]
          }, {
            "elementType": "labels.text.fill",
            "stylers": [{
              "saturation": 36
            }, {
              "color": "#333333"
            }, {
              "lightness": 40
            }]
          }, {
            "elementType": "labels.icon",
            "stylers": [{
              "visibility": "off"
            }]
          }, {
            "featureType": "transit",
            "elementType": "geometry",
            "stylers": [{
              "color": "#f2f2f2"
            }, {
              "lightness": 19
            }]
          }, {
            "featureType": "administrative",
            "elementType": "geometry.fill",
            "stylers": [{
              "color": "#fefefe"
            }, {
              "lightness": 20
            }]
          }, {
            "featureType": "administrative",
            "elementType": "geometry.stroke",
            "stylers": [{
              "color": "#fefefe"
            }, {
              "lightness": 17
            }, {
              "weight": 1.2
            }]
          }]

        }
      }
    },
      methods:{
        submitData(){
                 axios.post('http://localhost:8000/api/contact',this.form)
    .then(res => {
       this.form = ''
        console.log(res.data);
       this.$toastr.s('Message sent successfully.');
    })
        }
      },
  }
</script>
<style>
</style>
