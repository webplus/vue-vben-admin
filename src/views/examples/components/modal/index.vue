<script lang="tsx">
  import { defineComponent, unref } from 'compatible-vue';
  import { Alert } from 'ant-design-vue';
  import { useModal } from '@/components/modal/index';
  import { useDrawer } from '@/components/drawer/index';

  import Modal1 from './Modal1.vue';
  import Modal2 from './Modal2.vue';
  import Modal3 from './Modal3.vue';
  import Modal4 from './Modal4.vue';
  import Darwer1 from './Darwer1.vue';
  import Darwer2 from './Darwer2.vue';
  export default defineComponent({
    name: 'ModalDemo',
    setup() {
      const [register, { isFirstLoadRef, openModal }] = useModal();
      const [register2, { isFirstLoadRef: isFirstLoadRef2, openModal: openModal2 }] = useModal();
      const [register3, { isFirstLoadRef: isFirstLoadRef3, openModal: openModal3 }] = useModal();
      const [register4, { isFirstLoadRef: isFirstLoadRef4, openModal: openModal4 }] = useModal();

      const [registerDrawer, { isFirstLoadRef: isDrawerFirstLoadRef, openDrawer }] = useDrawer();
      const [
        registerDrawer1,
        { isFirstLoadRef: isDrawerFirstLoadRef1, openDrawer: openDrawer1 },
      ] = useDrawer();
      return () => {
        return (
          <div class="p-4 modal-demo">
            <Alert message="使用 useModal 进行弹窗操作，默认可以拖动，可以通过 draggable 参数进行控制是否可以拖动" />
            <a-button
              class="m-4"
              type="primary"
              onClick={() => {
                openModal({
                  visible: true,
                });
              }}
            >
              打开弹窗1(默认可以拖动)
            </a-button>
            <a-button
              class="m-4"
              type="primary"
              onClick={() => {
                openModal2({
                  visible: true,
                });
              }}
            >
              打开弹窗2(显示帮助按钮)
            </a-button>
            {!unref(isFirstLoadRef) && <Modal1 onRegister={register} />}
            {!unref(isFirstLoadRef2) && <Modal2 onRegister={register2} />}

            <Alert message="通过 useWrapper 参数进行控制是否可以自适应高度，默认打开" />
            <a-button
              class="m-4"
              type="primary"
              onClick={() => {
                openModal3({
                  visible: true,
                });
              }}
            >
              打开弹窗3(内容自适应屏幕高度)
            </a-button>
            {!unref(isFirstLoadRef3) && <Modal3 onRegister={register3} />}

            <Alert message="通过 canFullscreen 参数进行控制是否可以进行全屏，默认打开" />
            <a-button
              class="m-4"
              type="primary"
              onClick={() => {
                openModal4({
                  visible: true,
                });
              }}
            >
              打开弹窗4(控制弹窗是否可以全屏)
            </a-button>
            {!unref(isFirstLoadRef4) && <Modal4 onRegister={register4} />}

            <Alert message="drawer使用示例" />
            <a-button
              class="m-4"
              type="primary"
              onClick={() => {
                openDrawer({
                  visible: true,
                });
              }}
            >
              打开全屏drawer
            </a-button>
            {!unref(isDrawerFirstLoadRef) && <Darwer1 onRegister={registerDrawer} />}

            <a-button
              class="m-4"
              type="primary"
              onClick={() => {
                openDrawer1({
                  visible: true,
                });
              }}
            >
              打开局部drawer
            </a-button>
            {!unref(isDrawerFirstLoadRef1) && <Darwer2 onRegister={registerDrawer1} />}
          </div>
        );
      };
    },
  });
</script>
<style lang="less" scoped>
  .modal-demo {
    width: 100%;
  }
</style>
