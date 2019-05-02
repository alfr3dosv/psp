<template>
  <table style="font-family: 'Times New Roman';">
    <thead>

    <tr>
      <th>Summary</th>
      <th>Plan</th>
      <th>Actual</th>
      <th>To Date</th>
    </tr>
    </thead>
    <tbody>
    <tr>
      <td><strong>Program size</strong></td>
      <th>Plan</th>
      <th>Actual</th>
      <th>To Date</th>
    </tr>
    <tr>
      <td>Base(B)<span v-html="spaces"></span></td>
      <td class="i"><u><center><span v-html="spaces"/>{{summary.base.plan}}<span v-html="spaces"/></center></u></td>
      <td class="i"><u><center>{{summary.base.actual}}</center></u></td>
    </tr>
    <tr>
      <td>Deleted(D)<span v-html="spaces"/></td>
      <td class="i"><u><center><span v-html="spaces"/>{{summary.deleted.plan}}<span v-html="spaces"/></center></u></td>
      <td class="i"><u><center><span v-html="spaces"/>{{summary.deleted.actual}}<span v-html="spaces"/></center></u></td>
    </tr>
    <tr>
      <td>Modified(M)<span v-html="spaces"/></td>
      <td class="i"><u><center><span v-html="spaces"/>{{summary.modified.plan}}<span v-html="spaces"/></center></u></td>
      <td class="i"><u><center><span v-html="spaces"/>{{summary.modified.actual}}<span v-html="spaces"/></center></u></td>
    </tr>
    <tr>
      <td>Added(A)<span v-html="spaces"/></td>
      <td class="i"><u><center><span v-html="spaces"/>{{summary.added.actual}}<span v-html="spaces"/></center></u></td>
      <td class="i"><u><center><span v-html="spaces"/>{{summary.added.plan}}<span v-html="spaces"/></center></u></td>
    </tr>
    <tr>
      <td>Reused(R)<span v-html="spaces"/></td>
      <td class="i"><u><center><span v-html="spaces"/>{{summary.reused.actual}}<span v-html="spaces"/></center></u></td>
      <td class="i"><u><center><span v-html="spaces"/>{{summary.reused.plan}}<span v-html="spaces"/></center></u></td>
      <td class="i"><u><center><span v-html="spaces"/>228<span v-html="spaces"/></center></u></td></tr>
    <tr>
      <td>Added and Modified (A+M)<span v-html="spaces"></span></td>
      <td class="i"><u><center><span v-html="spaces"/>{{summary.addedAndModified.actual}}<span v-html="spaces"/></center></u></td>
      <td class="i"><u><center><span v-html="spaces"/>{{summary.addedAndModified.plan}}<span v-html="spaces"/></center></u></td>
      <td class="i"><u><center><span v-html="spaces"/>228<span v-html="spaces"/></center></u></td>
    </tr>
    <tr>
      <td>Total Size(T)<span v-html="spaces"></span></td>
      <td><u><center><span v-html="spaces"/>{{summary.totalSize.actual}}<span v-html="spaces"/></center></u></td>
      <td><u><center><span v-html="spaces"/>{{summary.totalSize.plan}}<span v-html="spaces"/></center></u></td>
      <td><u><center><span v-html="spaces"/>23<span v-html="spaces"/></center></u></td>
    </tr>
    <tr>
      <td>Total New Reusable<span v-html="spaces"></span></td>
      <td><u><center><span v-html="spaces"/>6<span v-html="spaces"/></center></u></td>
      <td><u><center><span v-html="spaces"/>2<span v-html="spaces"/></center></u></td>
      <td><u><center><span v-html="spaces"/>dsf<span v-html="spaces"/></center></u></td>
    </tr>
    <tr>

      <td><strong>Estimated Proxy Size(E)</strong></td>
      <td><u><center><span v-html="spaces"/>2<span v-html="spaces"/></center></u></td>

    </tr>
    </tbody>
  </table>
</template>

<script>
  export default {
    name: "SummaryPrint",
    props: ['summary'],
    data() {
      return {
        spaces: '&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'
      }
    }
  }
</script>

<style scoped>
.i {
  /*width: 150px;*/
  /*text-align: center;*/
  /*padding-left: 50px;*/
  /*padding-right: 50px;*/
}
</style>
