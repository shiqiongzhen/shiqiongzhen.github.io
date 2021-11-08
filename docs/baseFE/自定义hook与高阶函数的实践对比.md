## 第一层
```
<RenderModal
  title='asdasd'
  handleOk={(formdata) =>
    new Promise((resolve) => {
      console.log(1111, formdata);
      resolve(true);
    })
  }
  visable={visable}
  setVisable={setVisable}
/>
```

## 自定义 hook
> 第二层

```
import React, { useState, useEffect } from 'react';
import { Modal, Input, Form } from 'antd';
import useModal from './formWrapper';

export default Form.create({})(({ form, title, visable, setVisable, handleOk }) => {
  const { getFieldDecorator } = form;
  const { onOk, onCancel } = useModal({ form, setVisable, handleOk });
  return (
    <Modal title={title} onOk={onOk} onCancel={onCancel} visible={visable}>
      <Form>
        <Form.Item label='WIKI 地址'>
          {getFieldDecorator('caseUrl', {
            rules: [{ type: 'url', required: true, message: '请填写正确的链接地址' }]
          })(<Input.TextArea placeholder='https://123.sankuai.com/km/page/57491319' />)}
        </Form.Item>
      </Form>
    </Modal>
  );
});

```
> 第三层
```
import React, { useState, useEffect } from 'react';
import { Modal, Input, Form } from 'antd';

const RenderModal = ({ form, setVisable, handleOk }) => {
  const onOk = () => {
    form.validateFields((err, values) => {
      if (err) {
        return;
      }
      handleOk(values).then(() => {
        onCancel();
      });
    });
  };

  const onCancel = () => {
    setVisable(false);
  };

  return {
    onOk,
    onCancel
  };
};
export default RenderModal;
```

## 高阶组件
> 第二层
```
import React, { useState, useEffect } from 'react';
import { Modal, Input, Form } from 'antd';
import RenderModal from './formWrapper';

@RenderModal()
class FromComponent extends React.Component {
  render() {
    const { getFieldDecorator } = this.props.form;
    return (
      <Form>
        <Form.Item label='WIKI 地址'>
          {getFieldDecorator('caseUrl', {
            rules: [{ type: 'url', required: true, message: '请填写正确的链接地址' }]
          })(<Input.TextArea placeholder='https://123.sankuai.com/km/page/57491319' />)}
        </Form.Item>
      </Form>
    );
  }
}

export default Form.create({})(FromComponent);

```

> 第三层
```
export default () => (FromComponent) => {
  const RenderModal = ({ form, title, visable, setVisable, onOk }) => {
    const handleOk = () => {
      form.validateFields((err, values) => {
        if (err) {
          return;
        }
        onOk(values).then(() => {
          handleCancel();
        });
      });
    };

    const handleCancel = () => {
      setVisable(false);
    };
    console.log('title, visable', title, visable);
    
    return (
      <Modal title={title} onOk={handleOk} onCancel={handleCancel} visible={visable}>
        <FromComponent form={form} />
      </Modal>
    );
  };
  return RenderModal;
};
```