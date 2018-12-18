<template>
    <Page class="page">
        <ActionBar title="App" class="action-bar" />
        <ScrollView>
            <StackLayout class="home-panel">
                <!--Add your page content here-->
                <Button text="Scan NFC" @tap="goToScan" />
                <Label textWrap="true" text=" activate the nfc and bring a tag closer"
                    class="h2 description-label" />
            </StackLayout>
        </ScrollView>
    </Page>
</template>

<script>
import Home from './Home'
    export default {
      components: {
          Home
      },
      methods: {
          goToScan() {
              this.$navigateTo(Home)
          }
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