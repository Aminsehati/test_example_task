<template>
  <div class="note_item">
    <h3>
        {{
            noteItem.title
        }}
    </h3>
  </div>
</template>

<script>
export default {
    props:{
        noteItem:{
            type:Object,
            default:()=>{}
        }
    }
}
</script>

<style>
.note_item{
    border: 1px solid #ececec;
}
</style>