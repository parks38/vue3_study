<template>
    <div>
        <button @click="getPdfContent" data-id='Korean'>한국어</button>
        <button @click="getPdfContent" data-id='English'>영어</button>

    </div>
</template>

<script>
import { reactive, defineComponent } from "vue"
export default defineComponent({
  name: 'InfoContent',
  setup() {

    const pdfList = reactive({
        pdfList : [
            {
                index : 1,
                pdfPath : '/myfolder',
                attachTitle : 'Korean.pdf',
            },{
                index : 2,
                pdfPath : '/myfolder',
                attachTitle : 'English.pdf',
            }
        ]
    }); 
    
    const getPdfContent = (event) => {

        console.log(pdfList.pdfList[1].pdfPath);
        console.log(event.target.dataset.id);

        const path = pdfList.pdfList.filter(pdf => pdf.attachTitle.indexOf(event.target.dataset.id) >= 0);

        //console.log(path[0].pdfPath + '?filename=' + path[0].attachTitle);

        const urlLink = path[0].pdfPath + '?filename=' + path[0].attachTitle;

        window.open(urlLink);
        
    }

    return {
        getPdfContent, 
        pdfList,

    }
  }  
})

</script>

<style>
</style>