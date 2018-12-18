<template>
    <Page class="page">
        <ActionBar title="Home" class="action-bar" />
        <ScrollView>
            <StackLayout class="home-panel">
                <!--Add your page content here-->
                <Label textWrap="true" text="Play with NativeScript!" class="h2 description-label" />
                <Label textWrap="true" text=" activate the nfc and bring a tag closer"
                    class="h2 description-label" />
            </StackLayout>
        </ScrollView>
    </Page>
</template>

<script>
    var Nfc = require("nativescript-nfc").Nfc;  
    export default {
        data() {
            return {
                nfc: null
            };
        },
        mounted() {
            
            this.nfc = new Nfc();

            

            this.nfc.available().then(avail => {
                console.log(avail ? "Yes" : "No");
            });

            this.nfc.enabled().then(on => {
                console.log(on ? "Yes" : "No");
            });

            this.nfc.setOnNdefDiscoveredListener(
                    data => {
                        if (data.message) {
                            for (let m in data.message) {
                                let record = data.message[m];
                                console.log(
                                    "Ndef discovered! Message record: " +
                                    record.payloadAsString
                                );
                            }
                        }
                    }, {
                        // iOS-specific options
                        stopAfterFirstRead: true,
                        scanHint: "Scan a tag, baby!"
                    }
                )
                .then(() => {
                    console.log("OnNdefDiscovered listener added");
                });

            this.nfc.setOnTagDiscoveredListener(data => {
                    console.log("Discovered a tag with ID " + data.id);
                })
                .then(function() {
                    console.log("OnTagDiscovered listener added");
                });
                
        }
        
    };
</script>

<style scoped>
    .home-panel {
        vertical-align: center;
        font-size: 20;
        margin: 15;
    }

    .description-label {
        margin-bottom: 15;
    }
</style>