<template>
<main class="container container-height">
 <div class="card">
    <div class="card-body">
      <div class="row">
        <div class="col-md-12">
          <div class="row header-category-row mb-3">
            <div class="col-md-7 d-flex justify-content-start align-items-center"></div>
            <div class="col-md d-flex justify-content-end">
              <button type="button" @click="addRow" class="btn btn-success shadow-sm">+ Add New Record</button>
            </div>
          </div>
          <hr class="m-0 mt-2 mb-4" />
          <div class="card mt-2 mb-2" style="border-radius: 4px !important">
            <form v-on:submit.prevent="setDnsRecord">
              <div class="card-body p-2">
                <table class="table">
                  <thead class="mb-2">
                    <td style="width: 1%"></td>
                    <td style="width: 15%">Name</td>
                    <td style="width: 23%">Record Type</td>
                    <td style="width: 34%">Value</td>
                    <td style="width: 11%">Priority</td>
                    <td style="width: 12%">TTL</td>
                    <td></td>
                  </thead>
                  <tbody v-for="(data, index) in records" :key="index">
                    <tr v-if="data.record_type">
                      <td>
                        <p>{{ index }}</p>
                      </td>
                      <td>
                        <input :name="`records[${index}][name]`" type="text" class="form-control" v-model="data.name" placeholder="@ or www"/>
                      </td>
                      <td>
                        <select :name="`records[${index}][type]`" class="form-control" v-model="data.type">
                          <option value="A" :selected="data.record_type == 'A' ? true : false"> A (IP4 Address)</option>
                          <option value="AAAA" :selected=" data.record_type == 'AAAA' ? true : false"> AAAA (IP6 Address)</option>
                          <option value="MX" :selected="data.record_type == 'MX' ? true : false">MX (Mail)</option>
                          <option value="CNAME" :selected=" data.record_type == 'CNAME' ? true : false" > CNAME (Alias)</option>
                          <option value="TXT" :selected=" data.record_type == 'TXT' ? true : false"> SPF (TXT)</option>
                          <option value="SRV" :selected=" data.record_type == 'SRV' ? true : false"> SRV (Service)</option>
                        </select>
                      </td>
                      <td>
                        <input :name="`records[${index}][value]`" type="text" class="form-control" v-model="data.value" placeholder="Enter IP or hostname"/>
                      </td>
                      <td>
                        <input :name="`records[${index}][priority]`" type="text" class="form-control" v-model="data.priority" placeholder="0"/>
                      </td>
                      <td>
                        <input :name="`records[${index}][ttl]`" type="text" class="form-control" v-model="data.ttl" placeholder="3600"/>
                      </td>
                      <td>
                        <button type="button" class="close pointer btn-remove" v-show="hideRemoveBtn()" @click="removeRow(index)">-</button>
                      </td>
                    </tr>
                    <tr v-else>
                      <td>
                        <p>{{ index }}</p>
                      </td>
                      <td>
                        <input :name="`records[${index}][name]`" type="text" class="form-control" v-model="data.name" placeholder="@ or www" />
                      </td>
                      <td>
                        <select :name="`records[${index}][type]`" class="form-control" v-model="data.type">
                          <option value="A">A (IP4 Address)</option>
                          <option value="AAAA">AAAA (IP6 Address)</option>
                          <option value="MX">MX (Mail)</option>
                          <option value="CNAME">CNAME (Alias)</option>
                          <option value="TXT">SPF (TXT)</option>
                          <option value="SRV">SRV (Service)</option>
                        </select>
                      </td>
                      <td>
                        <input :name="`records[${index}][value]`" type="text" v-model="data.value" class="form-control" placeholder="Enter IP or hostname"/>
                      </td>
                      <td>
                        <input :name="`records[${index}][priority]`" type="text" v-model="data.priority" class="form-control" placeholder="0"/>
                      </td>
                      <td>
                        <input :name="`records[${index}][ttl]`" type="text" v-model="data.ttl" class="form-control" placeholder="3600"/>
                      </td>
                      <td>
                        <button  type="button" class="close pointer btn-remove" v-show="hideRemoveBtn()" title="Delete" @click="removeRow(index)">-</button>
                      </td>
                    </tr>
                  </tbody>
                </table>
              </div>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
    </main>
</template>

<script>
export default {
  name: 'DNSRecordForm',
  props: ['data'],
  data() {
    return {
      records: [],
      errors: [],
      message: [],
    };
  },
  methods: {
    addRow() {
      this.records.push({
        name: "",
        type: "A",
        value: "",
        priority: "",
        ttl :""
      });
    },

    hideRemoveBtn() {
      if (this.records.length == 0) {
        return false;
      }
      if (this.records.length > 1) {
        return true;
      }
    },

    removeRow(id) {
      if (this.records.length > 1) {
        this.records.splice(id, 1);
      }
    },

    cancelChanges() {
      
    },
 
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.btn-remove {
    border: none !important;
    opacity: 1;
    color: white;
    background: #c70704 !important;
    border-radius: 40% !important;
    padding: 0px 8px !important;

}

</style>
