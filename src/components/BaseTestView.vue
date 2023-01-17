<template>
  <v-container class="fill-height" @contextmenu="onContextMenu($event)">
    <v-responsive class="d-flex align-center text-center fill-height">

      <div class="text-body-2 font-weight-light mb-n1">Count {{ store.count }}</div>

      <div class="py-14" />

      <v-row class="d-flex align-center justify-center">
        <v-col cols="auto">
          <v-btn
            href="https://next.vuetifyjs.com/components/all/"
            min-width="164"
            rel="noopener noreferrer"
            target="_blank"
            variant="text"
          >
            <v-icon
              icon="mdi-view-dashboard"
              size="large"
              start
            />

            Components
          </v-btn>
        </v-col>

        <v-col cols="auto">
          <v-btn
            color="primary"
            href="https://next.vuetifyjs.com/introduction/why-vuetify/#feature-guides"
            min-width="228"
            rel="noopener noreferrer"
            size="x-large"
            target="_blank"
            variant="flat"
          >
            <v-icon
              icon="mdi-speedometer"
              size="large"
              start
            />

            Get Started
          </v-btn>
        </v-col>

        <v-col cols="auto">
          <v-btn
            href="https://community.vuetifyjs.com/"
            min-width="164"
            rel="noopener noreferrer"
            target="_blank"
            variant="text"
          >
            <v-icon
              icon="mdi-account-group"
              size="large"
              start
            />

            Community
          </v-btn>
        </v-col>
      </v-row>
    </v-responsive>

  dialog1Show: {{dialogs.dialog1Show}}
  dialogVMFormShow: {{dialogs.dialogVMFormShow}}
  <v-btn
    color="red lighten-2"
    dark
    @click.stop="dialogs.dialog1Show =  true"
  >
    ShowDialog1
  </v-btn>

  <dialog1 :dialogs="dialogs" @closeFnc="dialogs.dialog1Show=false"></dialog1>
  <dialog2 @close="dialog=false"></dialog2>
  <dialogTrans></dialogTrans>
  <dialogSimpleForm :dialogs="dialogs" @closeFormFnc="dialogs.dialogFormShow=false; testSimpleFormFnc();"></dialogSimpleForm>
  <dialogVModelForm :dialogs="dialogs" @closeFormFnc="dialogs.dialogVMFormShow=false; testVMFormFnc();"></dialogVModelForm>

  <dialogVMO 
    :visible="showVMForm"
    v-model:first_name="vmo_dialog_data.first_name"
    v-model:age="vmo_dialog_data.age"
    @closeVMOFnc="showVMForm=false;" @saveVMOFnc="showVMForm=false; testVMOFnc(vmo_dialog_data);"></dialogVMO> <!-- can access var here -->

  </v-container>

</template>

<script lang="ts" setup>
  import { onMounted, reactive, ref } from 'vue'

  import { MenuOptions } from '@imengyu/vue3-context-menu//src/ContextMenuDefine'
  import ContextMenu from '@imengyu/vue3-context-menu'
  import dialog1 from "@/components/DialogVmodel.vue"
  import dialog2 from "@/components/DialogParentAct.vue"
  import dialogTrans from "@/components/DialogTransition.vue"
  import dialogSimpleForm from "@/components/DialogSimpleForm.vue"
  import dialogVModelForm from "@/components/DialogVModelForm.vue"
  import dialogVMO from "@/components/DialogVModelObject.vue"

  import { useCounterStore } from "../store/counter"

  const store = useCounterStore();
  const dialogs = ref({
    dialog1Show: false,
    dialogFormShow: false,
    dialogVMFormShow: false,
  });

  const vmo_dialog_data = ref({
    first_name: "sample name",
    age: ""
  });

  const vee_form_data = ref({
    first_name: "",
    age: ""
  });
  const showVMForm = ref(false);
  const showVeeForm = ref(false);

  const menuData = reactive<MenuOptions>({
    items: [
      { 
        label: 'Simple item',
        onClick: () => { alert('Click Simple item'); store.increment(); },
      },
      {
        label: "Sub menu Example",
        children: [
          {
            label: "Show Dialog",
            onClick: () => {
               if (window.event) {
                  var isShift = !!window.event.shiftKey;
                  console.log("is shift: ", isShift);
               }
               dialogs.value.dialog1Show = true;
            }
          },
          {
            label: "Show VMO Form",
            onClick: () => {
               if (window.event) {
                  var isShift = !!window.event.shiftKey;
                  console.log("is shift: ", isShift);
               }
               showVMForm.value = true;
            }
          },
          { label: "Forward", disabled: true },
          { 
            label: "Reload", 
            divided: true, 
            icon: "icon-reload-1",
            onClick: () => {
              alert("You click Reload");
            }
          },
          { 
            label: "Save as...",
            icon: "icon-save",
            onClick: () => {
              alert("You click Save as");
            }
          },
          { 
            label: "Print...", 
            icon: "icon-print",
            onClick: () => {
              alert("You click Print");
            } 
          },
          { label: "View source", icon: "icon-terminal" },
          {
            label: "Show Dialog2",
            onClick: () => {
              this.dialog2 = true;
            }
          }
        ],
      },
      {
        label: "Submenu with Submenu",
        children: [
          {
            label: "Very long submenu",
            divided: true, 
            children: [
              { label: "Test1" },
              { label: "Test2" },
              { label: "Test3" },
              { label: "Test4" },
              { label: "Test5" },
              { label: "Test6" },
              { label: "Test7" },
              { label: "Test8" },
              { label: "Test9" },
              { label: "Test10" },
              { label: "Test11" },
              { label: "Test12" },
              { label: "Test13" },
              { label: "Test14" },
              { label: "Test15" },
              { label: "Test16" },
              { label: "Test17" },
              { label: "Test18" },
              { label: "Test19" },
              { label: "Test20" },
              { label: "Test21" },
              { label: "Test22" },
              { label: "Test23" },
              { label: "Test24" },
              { label: "Test25" },
              { label: "Test26" },
            ]
          },
          { 
            label: "A submenu", 
            children: [
              { label: "日本語の基礎" },
              { label: "Item2" },
              { label: "Item3" },
            ]
          },
          { 
            label: "A submenu2", 
            children: [
              { label: "Item1" },
              { label: "Item2" },
              { label: "Item3" },
              { 
                label: "A submenu", 
                children: [
                  { label: "Item1" },
                  { label: "Item2" },
                  { label: "Item3" },
                ]
              },
            ]
          },
        ]
      },
      { 
        label: 'Test item dynamic show and hide',
        clickClose: false,
        onClick: () => {
          menuData.items[4].hidden = !menuData.items[4].hidden;
        },
      },
      { 
        label: 'Click the item above to show/hide me',
      },
      { 
        label: 'Test item dynamic change the label',
        clickClose: false,
        onClick: () => {
          if (menuData.items[5].label === 'Test item dynamic change the label')
            menuData.items[5].label = 'My label CHANGED!';
          else
            menuData.items[5].label = 'Test item dynamic change the label';
        },
      },
      { 
        label: 'Item with icon',
        icon: "icon-reload-1",
      },
      { 
        label: "Item with svg icon",
        svgIcon: "#icon-clock",
      },
      { 
        label: "Item with svg icon",
        svgIcon: "#icon-multiply",
        svgProps: {
          fill: '#f60',
        },
      },
    ],
    iconFontClass: 'iconfont',
    customClass: "class-a",
    zIndex: 3,
    minWidth: 230,
    x: 0,
    y: 0,
  });
  function onContextMenu(e : MouseEvent) {
    //prevent the browser's default menu
    e.preventDefault();

    if (store.count == 0) {
      menuData.x = e.x;
      menuData.y = e.y;
      //show our menu
      ContextMenu.showContextMenu(menuData);
    }
    else {
      //menuData2.x = e.x;
      //menuData2.y = e.y;
      const menuData2 = {
          items: [
            { 
              label: 'This is menu in child box',
            },
            { 
              label: 'Simple item',
            },
          ],
          iconFontClass: 'iconfont',
          customClass: "class-a",
          zIndex: 3,
          minWidth: 230,
          x: e.x,
          y: e.y
        } as MenuOptions;
      ContextMenu.showContextMenu(menuData2);

    }

  }

</script>

<script lang="ts">
  export default {

    methods: {
      testSimpleFormFnc() {
        if (!document.getElementById('dialogForm')) {
          alert('No form exists');
          return;
        }
        let first_name =  document.getElementById('dialogForm').querySelector('#first_name');
        let age =  document.getElementById('dialogForm').querySelector('#age');
        alert('Hi ' + first_name.value + ', ' + age.value + ' tuoi');
      },
      testVMFormFnc() {
        alert('Hi ' + first_name.value + ', ' + age.value + ' tuoi');
      },
      testVMOFnc: function(test_var) {
        console.log(test_var.first_name);
        //we can't access vmo_dialog_data in this scope
      },
      testVeeFnc: function(test_var) {
        console.log(test_var.first_name);
        //we can't access vmo_dialog_data in this scope
      }
    },

  }
</script>