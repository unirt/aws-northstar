### Notes

From release [v1.3.0](https://github.com/aws/aws-northstar/releases/tag/v1.3.0), the implementation of FormRenderer MarkdownEditor and FormRenderer Table has been extracted out as seperate pluggable components to reduce the build bundle size of the consumer applications.

If your application uses MarkdownEditor in the FormRenderer, you will need to import it explictly via customCopmonentMapping prop:
 
```jsx static
import React from 'react';
...
import FormRendererMarkdownEditor from '../FormRendererMarkdownEditor';
...

const customComponentMapping = {
    "MARKDOWN_EDITOR": FormRendererMarkdownEditor
}

return (
    <FormRenderer 
        schema={schema} 
        customComponentWrapper={customComponentMapping}
        onSubmit={...} 
        onCancel={...} />);
```

### Examples

**More examples** are available on <a href="https://storybook.northstar.aws-prototyping.cloud/?path=/story/formrenderer" target="_blank">NorthStar Storybook</a>.

```jsx
import FormRenderer, { componentTypes, validatorTypes } from 'aws-northstar/components/FormRenderer';
import Container from 'aws-northstar/layouts/Container';
import { awsServices } from '../Autosuggest/data/data';

const treeItems = {
    id: '1',
    label: 'Tree Root',
    children: [
        {
            id: '2',
            label: 'Node 1.0',
            children: [
                { id: '3', label: 'Node 1.1' },
                { id: '4', label: 'Node 1.3' },
            ],
        },
        {
            id: '5',
            label: 'Node 2.0',
            children: [
                {
                    id: '6',
                    label: 'Node 2.1.0',
                    children: [{ id: '7', label: 'Node 2.1.2' }],
                },
                { id: '8', label: 'Node 2.2' },
            ],
        },
    ],
};

const schema = {
    fields: [
        {
            component: componentTypes.TEXT_FIELD,
            name: 'email',
            label: 'Email',
            isRequired: true,
            validate: [
                {
                    type: validatorTypes.REQUIRED,
                },
                {
                    type: validatorTypes.PATTERN,
                    message: 'Invalid email address',
                    pattern: /^(?:[a-z0-9!#$%&'*+/=?^_`{|}~-]+(?:\.[a-z0-9!#$%&'*+/=?^_`{|}~-]+)*|"(?:[\x01-\x08\x0b\x0c\x0e-\x1f\x21\x23-\x5b\x5d-\x7f]|\\[\x01-\x09\x0b\x0c\x0e-\x7f])*")@(?:(?:[a-z0-9](?:[a-z0-9-]*[a-z0-9])?\.)+[a-z0-9](?:[a-z0-9-]*[a-z0-9])?|\[(?:(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.){3}(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?|[a-z0-9-]*[a-z0-9]:(?:[\x01-\x08\x0b\x0c\x0e-\x1f\x21-\x5a\x53-\x7f]|\\[\x01-\x09\x0b\x0c\x0e-\x7f])+)\])$/i,
                },
            ],
        },
        {
            component: componentTypes.TEXT_FIELD,
            name: 'password',
            label: 'Password',
            type: 'password',
            isRequired: true,
            validate: [
                {
                    type: validatorTypes.REQUIRED,
                },
                {
                    type: validatorTypes.MIN_LENGTH,
                    threshold: 6,
                },
                {
                    type: validatorTypes.MAX_LENGTH,
                    threshold: 10,
                },
            ],
        },
        {
            component: componentTypes.TEXT_FIELD,
            name: 'number',
            label: 'Number',
            type: 'number',
            validate: [
                {
                    type: validatorTypes.MIN_NUMBER_VALUE,
                    includeThreshold: true,
                    value: 4,
                },
                {
                    type: validatorTypes.MAX_NUMBER_VALUE,
                    includeThreshold: false,
                    value: 20,
                },
            ],
        },
        {
            component: componentTypes.CHECKBOX,
            name: 'checkbox',
            label: 'Checkbox',
            options: [
                {
                    label: 'Option 1',
                    value: '1',
                },
                {
                    label: 'Option 2',
                    value: '2',
                },
                {
                    label: 'Option 3',
                    value: '3',
                },
            ],
            isRequired: true,
            validate: [
                {
                    type: validatorTypes.REQUIRED,
                },
            ],
        },
        {
            component: componentTypes.RADIO,
            name: 'radio',
            label: 'Radio',
            options: [
                {
                    label: 'Option 1',
                    value: '1',
                },
                {
                    label: 'Option 2',
                    value: '2',
                },
                {
                    label: 'Option 3',
                    value: '3',
                },
            ],
            isRequired: true,
            validate: [
                {
                    type: validatorTypes.REQUIRED,
                },
            ],
        },
        {
            component: componentTypes.SELECT,
            name: 'select',
            label: 'Select',
            placeholder: 'Choose an option',
            options: [
                {
                    label: 'Option 1',
                    value: '1',
                },
                {
                    label: 'Option 2',
                    value: '2',
                },
                {
                    label: 'Option 3',
                    value: '3',
                },
            ],
            isRequired: true,
            validate: [
                {
                    type: validatorTypes.REQUIRED,
                },
            ],
        },
        {
            component: componentTypes.SELECT,
            name: 'autosugguest',
            label: 'Autosuggest',
            placeholder: 'Choose an AWS service',
            isSearchable: true,
            options: awsServices,
            isRequired: true,
            validate: [
                {
                    type: validatorTypes.REQUIRED,
                },
            ],
        },
        {
            component: componentTypes.SELECT,
            name: 'multiselect',
            label: 'Multiselect',
            placeholder: 'Choose an AWS service',
            multiSelect: true,
            options: awsServices,
            isRequired: true,
            checkboxes: true,
            validate: [
                {
                    type: validatorTypes.REQUIRED,
                },
            ],
        },
        {
            component: componentTypes.TEXTAREA,
            name: 'textarea',
            label: 'Textarea',
            helperText: 'This is a help text',
            isRequired: true,
            validate: [
                {
                    type: validatorTypes.REQUIRED,
                },
            ],
        },
        {
            component: componentTypes.SWITCH,
            name: 'switch',
            label: 'Switch',
        },
        {
            component: componentTypes.SWITCH,
            name: 'switch1',
            label: 'Switch 1',
        },
        {
            component: componentTypes.SWITCH,
            name: 'switch2',
            label: 'Switch 2',
        },
        {
            component: componentTypes.DATE_PICKER,
            name: 'datePicker',
            label: 'Date picker',
            isRequired: true,
            validate: [
                {
                    type: validatorTypes.REQUIRED,
                },
            ],
        },
        {
            component: componentTypes.TIME_PICKER,
            name: 'timePicker',
            label: 'Time picker',
            isRequired: true,
            validate: [
                {
                    type: validatorTypes.REQUIRED,
                },
            ],
        },
        {
            component: componentTypes.TREE_VIEW,
            label: 'this is a tree',
            helperText: 'this is a hint',
            description: 'this is a description',
            name: 'tree',
            treeItems: treeItems,
            multiSelect: true,
            defaultExpanded: ['1', '2'],
            validate: [
                {
                    type: validatorTypes.REQUIRED,
                },
            ],
        },
        {
            component: componentTypes.CHECKBOX,
            name: 'confirm',
            label: 'I understand the terms and condition',
            description: 'Term 1.0.0',
            validate: [
                {
                    type: validatorTypes.REQUIRED,
                    message: 'please accept the terms and condition',
                },
            ],
        },
    ],
    header: 'Data driven form',
    description: 'Define your form in json format',
};
    
<Container>
    <FormRenderer schema={schema} onSubmit={console.log} onCancel={console.log} />
</Container>
```

```jsx
import FormRenderer, { componentTypes, validatorTypes } from 'aws-northstar/components/FormRenderer';
import Container from 'aws-northstar/layouts/Container';
import { awsServices } from '../Autosuggest/data/data';

const initialValues = {
    email: 'test@test.com',
    password: 'password',
    number: 10,
    textarea: 'textarea',
    checkbox: ['1', '2'],
    switch: true,
    radio: '3',
    select: '2',
    autosugguest: {
        value: 'Lambda',
        label: 'Lambda - Amazon Lambda',
    },
    multiselect: [
        {
            value: 'Lambda',
            label: 'Lambda - Amazon Lambda',
        },
        {
            value: 'EC2',
            label: 'EC2 - Amazon Elastic Compute Cloud',
        },
    ],
    confirm: true,
    datePicker: new Date(2020, 1, 1),
    timePicker: '2020-01-01T00:00:00Z',
    tree: ['3', '5'],
};

const treeItems = {
    id: '1',
    label: 'Tree Root',
    children: [
        {
            id: '2',
            label: 'Node 1.0',
            children: [
                { id: '3', label: 'Node 1.1' },
                { id: '4', label: 'Node 1.3' },
            ],
        },
        {
            id: '5',
            label: 'Node 2.0',
            children: [
                {
                    id: '6',
                    label: 'Node 2.1.0',
                    children: [{ id: '7', label: 'Node 2.1.2' }],
                },
                { id: '8', label: 'Node 2.2' },
            ],
        },
    ],
};

const schema = {
    fields: [
        {
            component: componentTypes.TEXT_FIELD,
            name: 'email',
            label: 'Email',
            isRequired: true,
            validate: [
                {
                    type: validatorTypes.REQUIRED,
                },
                {
                    type: validatorTypes.PATTERN,
                    message: 'Invalid email address',
                    pattern: /^(?:[a-z0-9!#$%&'*+/=?^_`{|}~-]+(?:\.[a-z0-9!#$%&'*+/=?^_`{|}~-]+)*|"(?:[\x01-\x08\x0b\x0c\x0e-\x1f\x21\x23-\x5b\x5d-\x7f]|\\[\x01-\x09\x0b\x0c\x0e-\x7f])*")@(?:(?:[a-z0-9](?:[a-z0-9-]*[a-z0-9])?\.)+[a-z0-9](?:[a-z0-9-]*[a-z0-9])?|\[(?:(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.){3}(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?|[a-z0-9-]*[a-z0-9]:(?:[\x01-\x08\x0b\x0c\x0e-\x1f\x21-\x5a\x53-\x7f]|\\[\x01-\x09\x0b\x0c\x0e-\x7f])+)\])$/i,
                },
            ],
        },
        {
            component: componentTypes.TEXT_FIELD,
            name: 'password',
            label: 'Password',
            type: 'password',
            isRequired: true,
            validate: [
                {
                    type: validatorTypes.REQUIRED,
                },
                {
                    type: validatorTypes.MIN_LENGTH,
                    threshold: 6,
                },
                {
                    type: validatorTypes.MAX_LENGTH,
                    threshold: 10,
                },
            ],
        },
        {
            component: componentTypes.TEXT_FIELD,
            name: 'number',
            label: 'Number',
            type: 'number',
            validate: [
                {
                    type: validatorTypes.MIN_NUMBER_VALUE,
                    includeThreshold: true,
                    value: 4,
                },
                {
                    type: validatorTypes.MAX_NUMBER_VALUE,
                    includeThreshold: false,
                    value: 20,
                },
            ],
        },
        {
            component: componentTypes.CHECKBOX,
            name: 'checkbox',
            label: 'Checkbox',
            options: [
                {
                    label: 'Option 1',
                    value: '1',
                },
                {
                    label: 'Option 2',
                    value: '2',
                },
                {
                    label: 'Option 3',
                    value: '3',
                },
            ],
            isRequired: true,
            validate: [
                {
                    type: validatorTypes.REQUIRED,
                },
            ],
        },
        {
            component: componentTypes.RADIO,
            name: 'radio',
            label: 'Radio',
            options: [
                {
                    label: 'Option 1',
                    value: '1',
                },
                {
                    label: 'Option 2',
                    value: '2',
                },
                {
                    label: 'Option 3',
                    value: '3',
                },
            ],
            isRequired: true,
            validate: [
                {
                    type: validatorTypes.REQUIRED,
                },
            ],
        },
        {
            component: componentTypes.SELECT,
            name: 'select',
            label: 'Select',
            placeholder: 'Choose an option',
            options: [
                {
                    label: 'Option 1',
                    value: '1',
                },
                {
                    label: 'Option 2',
                    value: '2',
                },
                {
                    label: 'Option 3',
                    value: '3',
                },
            ],
            isRequired: true,
            validate: [
                {
                    type: validatorTypes.REQUIRED,
                },
            ],
        },
        {
            component: componentTypes.SELECT,
            name: 'autosugguest',
            label: 'Autosuggest',
            placeholder: 'Choose an AWS service',
            isSearchable: true,
            options: awsServices,
            isRequired: true,
            validate: [
                {
                    type: validatorTypes.REQUIRED,
                },
            ],
        },
        {
            component: componentTypes.SELECT,
            name: 'multiselect',
            label: 'Multiselect',
            placeholder: 'Choose an AWS service',
            multiSelect: true,
            options: awsServices,
            isRequired: true,
            checkboxes: true,
            validate: [
                {
                    type: validatorTypes.REQUIRED,
                },
            ],
        },
        {
            component: componentTypes.TEXTAREA,
            name: 'textarea',
            label: 'Textarea',
            helperText: 'This is a help text',
            isRequired: true,
            validate: [
                {
                    type: validatorTypes.REQUIRED,
                },
            ],
        },
        {
            component: componentTypes.SWITCH,
            name: 'switch',
            label: 'Switch',
        },
        {
            component: componentTypes.SWITCH,
            name: 'switch1',
            label: 'Switch 1',
        },
        {
            component: componentTypes.SWITCH,
            name: 'switch2',
            label: 'Switch 2',
        },
        {
            component: componentTypes.DATE_PICKER,
            name: 'datePicker',
            label: 'Date picker',
            isRequired: true,
            validate: [
                {
                    type: validatorTypes.REQUIRED,
                },
            ],
        },
        {
            component: componentTypes.TIME_PICKER,
            name: 'timePicker',
            label: 'Time picker',
            isRequired: true,
            validate: [
                {
                    type: validatorTypes.REQUIRED,
                },
            ],
        },
        {
            component: componentTypes.TREE_VIEW,
            label: 'this is a tree',
            helperText: 'this is a hint',
            description: 'this is a description',
            name: 'tree',
            treeItems: treeItems,
            multiSelect: true,
            defaultExpanded: ['1', '2'],
            validate: [
                {
                    type: validatorTypes.REQUIRED,
                },
            ],
        },
        {
            component: componentTypes.CHECKBOX,
            name: 'confirm',
            label: 'I understand the terms and condition',
            description: 'Term 1.0.0',
            validate: [
                {
                    type: validatorTypes.REQUIRED,
                    message: 'please accept the terms and condition',
                },
            ],
        },
    ],
    header: 'Data driven form with initial values',
    description: 'Define your form in json format',
};
    
<Container>
    <FormRenderer schema={schema} initialValues={initialValues} onSubmit={console.log} onCancel={console.log} />
</Container>
```

```jsx 
import FormRenderer, { componentTypes, validatorTypes } from 'aws-northstar/components/FormRenderer';
import Container from 'aws-northstar/layouts/Container';

const schema = {
    fields: [
        {
            component: componentTypes.SUB_FORM,
            title: 'Subform 1',
            description: 'This is a subform',
            name: 'subform1',
            fields: [
                {
                    component: componentTypes.TEXT_FIELD,
                    name: 'name1',
                    label: 'Name',
                    validate: [
                        {
                            type: validatorTypes.REQUIRED,
                        },
                    ],
                },
                {
                    component: componentTypes.EXPANDABLE_SECTION,
                    title: 'Additional information',
                    description: 'This is for additional information',
                    name: 'additionalInfo',
                    fields: [
                        {
                            component: componentTypes.TEXT_FIELD,
                            name: 'username',
                            label: 'Username',
                            validate: [
                                {
                                    type: validatorTypes.REQUIRED,
                                },
                            ],
                        },
                    ],
                },
            ],
        },
        {
            component: componentTypes.EXPANDABLE_SECTION,
            title: 'Subform 2',
            description: 'This is a expandable subform',
            name: 'subform2',
            variant: 'container',
            fields: [
                {
                    component: componentTypes.TEXT_FIELD,
                    name: 'name2',
                    label: 'Name',
                    validate: [
                        {
                            type: validatorTypes.REQUIRED,
                        },
                    ],
                },
            ],
        },
        {
            component: componentTypes.EXPANDABLE_SECTION,
            title: 'Subform 3',
            description: 'This is a expanded expandable subform',
            name: 'subform3',
            expandable: true,
            expanded: true,
            variant: 'container',
            fields: [
                {
                    component: componentTypes.SELECT,
                    name: 'select',
                    label: 'Select',
                    placeholder: 'Choose an option',
                    options: [
                        {
                            label: 'Option 1',
                            value: '1',
                        },
                        {
                            label: 'Option 2',
                            value: '2',
                        },
                        {
                            label: 'Option 3',
                            value: '3',
                        },
                    ],
                    isRequired: true,
                    validate: [
                        {
                            type: validatorTypes.REQUIRED,
                        },
                    ],
                },
            ],
        },
    ],
    header: 'Data driven form with subforms',
    description: 'Define your form in json format',
};

<Container>
    <FormRenderer schema={schema} onSubmit={console.log} onCancel={console.log} />
</Container>
``` 

```jsx
import FormRenderer, { componentTypes, validatorTypes } from 'aws-northstar/components/FormRenderer';
import Container from 'aws-northstar/layouts/Container';

const schema = {
    fields: [
        {
            component: componentTypes.SUB_FORM,
            title: 'Subform 1',
            description: 'This is a subform',
            name: 'subform1',
            fields: [
                {
                    component: componentTypes.FIELD_ARRAY,
                    label: 'Attribute Editor',
                    description: 'This is a form array',
                    name: 'fieldArray',
                    helperText: 'You can add up to 6 more items.',
                    minItems: 4,
                    maxItems: 6,
                    noItemsMessage: 'Please add new item',
                    defaultItem: {
                        key: 'key',
                        value: 'value',
                        type: 'type1',
                    },
                    validate: [
                        {
                            type: validatorTypes.MIN_ITEMS,
                            threshold: 4,
                        },
                        {
                            type: validatorTypes.REQUIRED,
                        },
                    ],
                    fields: [
                        {
                            component: componentTypes.TEXT_FIELD,
                            name: 'key',
                            label: 'Key',
                            validate: [
                                {
                                    type: validatorTypes.REQUIRED,
                                },
                            ],
                        },
                        {
                            component: componentTypes.TEXT_FIELD,
                            name: 'value',
                            label: 'Value',
                            validate: [
                                {
                                    type: validatorTypes.REQUIRED,
                                },
                            ],
                        },
                        {
                            component: componentTypes.SELECT,
                            name: 'type',
                            label: 'Type',
                            placeholder: 'Choose the type',
                            options: [
                                { label: 'Type 1', value: 'type1' },
                                { label: 'Type 2', value: 'type2' },
                                { label: 'Type 3', value: 'type3' },
                            ],
                            validate: [
                                {
                                    type: validatorTypes.REQUIRED,
                                },
                            ],
                        },
                    ],
                },
            ],
        },
        {
            component: componentTypes.SUB_FORM,
            title: 'Subform 2',
            description: 'This is a subform',
            name: 'subform2',
            fields: [
                {
                    component: componentTypes.FIELD_ARRAY,
                    label: 'Attribute Editor',
                    description: 'This is a form array',
                    name: 'fieldArray1',
                    helperText: 'You can add up to 6 more items.',
                    minItems: 3,
                    maxItems: 6,
                    noItemsMessage: 'Please add new item',
                    defaultItem: {
                        key: 'key',
                        value: 'value',
                        type: 'type1',
                    },
                    validate: [
                        {
                            type: validatorTypes.MIN_ITEMS,
                            threshold: 3,
                        },
                    ],
                    fields: [
                        {
                            component: componentTypes.TEXT_FIELD,
                            name: 'key',
                            label: 'Key',
                            validate: [
                                {
                                    type: validatorTypes.REQUIRED,
                                },
                            ],
                        },
                        {
                            component: componentTypes.TEXT_FIELD,
                            name: 'value',
                            label: 'Value',
                            validate: [
                                {
                                    type: validatorTypes.REQUIRED,
                                },
                            ],
                        },
                        {
                            component: componentTypes.SELECT,
                            name: 'type',
                            label: 'Type',
                            placeholder: 'Choose the type',
                            options: [
                                { label: 'Type 1', value: 'type1' },
                                { label: 'Type 2', value: 'type2' },
                                { label: 'Type 3', value: 'type3' },
                            ],
                            validate: [
                                {
                                    type: validatorTypes.REQUIRED,
                                },
                            ],
                        },
                    ],
                },
            ],
        },
        {
            component: componentTypes.SUB_FORM,
            title: 'Subform 3',
            description: 'This is a subform',
            name: 'subform3',
            fields: [
                {
                    component: componentTypes.FIELD_ARRAY,
                    label: 'Attribute Editor',
                    description: 'This is a readonly form array',
                    name: 'readonlyFieldArray',
                    isReadOnly: true,
                    fields: [
                        {
                            component: componentTypes.TEXT_FIELD,
                            name: 'key',
                            label: 'Key',
                            isReadOnly: true,
                            validate: [
                                {
                                    type: validatorTypes.REQUIRED,
                                },
                            ],
                        },
                        {
                            component: componentTypes.TEXT_FIELD,
                            name: 'value',
                            label: 'Value',
                            isReadOnly: true,
                            validate: [
                                {
                                    type: validatorTypes.REQUIRED,
                                },
                            ],
                        },
                        {
                            component: componentTypes.SELECT,
                            name: 'type',
                            label: 'Type',
                            placeholder: 'Choose the type',
                            isReadOnly: true,
                            options: [
                                { label: 'Type 1', value: 'type1' },
                                { label: 'Type 2', value: 'type2' },
                                { label: 'Type 3', value: 'type3' },
                            ],
                            validate: [
                                {
                                    type: validatorTypes.REQUIRED,
                                },
                            ],
                        },
                    ],
                },
            ],
        },
    ],
    header: 'Data driven form with field arrays',
    description: 'Define your form in json format',
};

const initialValues = {
    fieldArray: [
        { key: 'key1', value: 'value1', type: 'type1' },
        { key: 'key2', value: 'value2', type: 'type2' },
        { key: 'key3', value: 'value3', type: 'type3' },
    ],
    readonlyFieldArray: [
        { key: 'key1', value: 'value1', type: 'type1' },
        { key: 'key2', value: 'value2', type: 'type2' },
        { key: 'key3', value: 'value3', type: 'type3' },
        { key: 'key4', value: 'value4', type: 'type1' },
    ],
};

<Container>
    <FormRenderer
        schema={schema}
        onSubmit={console.log}
        onCancel={console.log}
        initialValues={initialValues}
    />
</Container>
```

```jsx
import FormRenderer, { componentTypes, validatorTypes } from 'aws-northstar/components/FormRenderer';
import Container from 'aws-northstar/layouts/Container';
import Box from 'aws-northstar/layouts/Box';
import FormRendererTable from 'aws-northstar/components/FormRendererTable';

const ReviewTemplate = (data) => {
    return <Box>{JSON.stringify(data)}</Box>;
};

const customComponentMapping = {
    'TABLE': FormRendererTable
}

const schema = {
    fields: [
        {
            component: componentTypes.WIZARD,
            name: 'wizzard',
            submitButtonText: 'Custom Submit Label',
            fields: [
                {
                    name: 'step-1',
                    title: 'Step 1',
                    description: 'Descrirption for Step 1',
                    fields: [
                        {
                            component: componentTypes.TEXTAREA,
                            name: 'textarea',
                            label: 'Textarea',
                            validate: [
                                {
                                    type: validatorTypes.REQUIRED,
                                },
                            ],
                        },
                        {
                            component: componentTypes.SELECT,
                            name: 'type',
                            label: 'Type',
                            placeholder: 'Choose the type',
                            options: [
                                { label: 'Type 1', value: 'type1' },
                                { label: 'Type 2', value: 'type2' },
                                { label: 'Type 3', value: 'type3' },
                            ],
                            validate: [
                                {
                                    type: validatorTypes.REQUIRED,
                                },
                            ],
                        },
                        {
                            component: componentTypes.EXPANDABLE_SECTION,
                            title: 'Additional information',
                            description: 'This is for additional information',
                            name: 'additionalInfo',
                            variant: 'default',
                            fields: [
                                {
                                    component: componentTypes.TEXT_FIELD,
                                    name: 'username',
                                    label: 'Username',
                                    expandable: true,
                                    validate: [
                                        {
                                            type: validatorTypes.REQUIRED,
                                        },
                                    ],
                                },
                            ],
                        },
                    ],
                },
                {
                    name: 'step-2',
                    title: 'Step 2',
                    fields: [
                        {
                            component: componentTypes.CHECKBOX,
                            name: 'checkbox',
                            label: 'Checkbox',
                            options: [
                                {
                                    label: 'Option 1',
                                    value: '1',
                                },
                                {
                                    label: 'Option 2',
                                    value: '2',
                                },
                                {
                                    label: 'Option 3',
                                    value: '3',
                                },
                            ],
                            isRequired: true,
                            validate: [
                                {
                                    type: validatorTypes.REQUIRED,
                                },
                            ],
                        },
                        {
                            component: componentTypes.RADIO,
                            name: 'radio',
                            label: 'Radio',
                            options: [
                                {
                                    label: 'Option 1',
                                    value: '1',
                                },
                                {
                                    label: 'Option 2',
                                    value: '2',
                                },
                                {
                                    label: 'Option 3',
                                    value: '3',
                                },
                            ],
                            isRequired: true,
                            validate: [
                                {
                                    type: validatorTypes.REQUIRED,
                                },
                            ],
                        },
                        {
                            component: componentTypes.FIELD_ARRAY,
                            label: 'Attribute Editor',
                            description: 'This is a form array',
                            name: 'fieldArray',
                            helperText: 'You can add up to 6 more items.',
                            minItems: 4,
                            maxItems: 6,
                            noItemsMessage: 'Please add new item',
                            defaultItem: {
                                key: 'key',
                                value: 'value',
                                type: 'type1',
                            },
                            validate: [
                                {
                                    type: validatorTypes.MIN_ITEMS,
                                    threshold: 4,
                                },
                                {
                                    type: validatorTypes.REQUIRED,
                                },
                            ],
                            fields: [
                                {
                                    component: componentTypes.TEXT_FIELD,
                                    name: 'key',
                                    label: 'Key',
                                    validate: [
                                        {
                                            type: validatorTypes.REQUIRED,
                                        },
                                    ],
                                },
                                {
                                    component: componentTypes.TEXT_FIELD,
                                    name: 'value',
                                    label: 'Value',
                                    validate: [
                                        {
                                            type: validatorTypes.REQUIRED,
                                        },
                                    ],
                                },
                                {
                                    component: componentTypes.SELECT,
                                    name: 'type',
                                    label: 'Type',
                                    placeholder: 'Choose the type',
                                    options: [
                                        { label: 'Type 1', value: 'type1' },
                                        { label: 'Type 2', value: 'type2' },
                                        { label: 'Type 3', value: 'type3' },
                                    ],
                                    validate: [
                                        {
                                            type: validatorTypes.REQUIRED,
                                        },
                                    ],
                                },
                            ],
                        },
                    ],
                },
                {
                    name: 'step-3',
                    title: 'Step 3',
                    fields: [
                        {
                            component: componentTypes.TEXT_FIELD,
                            name: 'name1',
                            label: 'Name',
                            validate: [
                                {
                                    type: validatorTypes.REQUIRED,
                                },
                            ],
                        },
                        {
                            component: componentTypes.SWITCH,
                            name: 'switch',
                            label: 'Switch',
                        },
                        {
                            component: componentTypes.DATE_PICKER,
                            name: 'datePicker',
                            label: 'Date picker',
                            isRequired: true,
                            validate: [
                                {
                                    type: validatorTypes.REQUIRED,
                                },
                            ],
                        },
                        {
                            component: componentTypes.TIME_PICKER,
                            name: 'timePicker',
                            label: 'Time picker',
                            isRequired: true,
                            validate: [
                                {
                                    type: validatorTypes.REQUIRED,
                                },
                            ],
                        },
                        {
                            component: componentTypes.CHECKBOX,
                            name: 'confirm',
                            label: 'I understand the terms and condition',
                            description: 'Term 1.0.0',
                            validate: [
                                {
                                    type: validatorTypes.REQUIRED,
                                    message: 'please accept the terms and condition',
                                },
                            ],
                        },
                    ],
                },
                {
                    name: 'step-4',
                    title: 'Step 4',
                    fields: [
                        {
                            component: 'TABLE',
                            name: 'table',
                            label: 'Table',
                            description: 'This is a table',
                            getRowId: data => data.id,
                            items: [
                                {
                                    id: 'id0000011',
                                    name: 'Engagement 11',
                                    createdDate: '2019-10-12',
                                },
                                {
                                    id: 'id0000012',
                                    name: 'Engagement 12',
                                    createdDate: '2019-11-12',
                                },
                                {
                                    id: 'id0000013',
                                    name: 'Engagement 13',
                                    createdDate: '2020-01-01',
                                },
                            ],
                            columnDefinitions: [
                                {
                                    id: 'id',
                                    width: 200,
                                    Header: 'Id',
                                    accessor: 'id',
                                },
                                {
                                    id: 'name',
                                    width: 200,
                                    Header: 'Name',
                                    accessor: 'name',
                                },
                                {
                                    id: 'createdDate',
                                    width: 200,
                                    Header: 'Created date',
                                    accessor: 'createdDate',
                                },
                            ],
                            validate: [
                                {
                                    type: validatorTypes.REQUIRED,
                                },
                            ],
                        },
                    ],
                },
                {
                    name: 'step-5',
                    title: 'Review',
                    fields: [
                        {
                            component: componentTypes.REVIEW,
                            name: 'review',
                            Template: ReviewTemplate,
                        },
                    ],
                },
            ],
        },
    ],
    header: 'Data driven form with wizard',
    description: 'Define your form in json format',
};

const initialValues = {
    textarea: 'textarea',
    type: 'type1',
    additionalInfo: { username: 'username' },
    checkbox: ['1'],
    radio: '1',
    fieldArray: [
        { key: 'key1', value: 'value1', type: 'type1' },
        { key: 'key2', value: 'value2', type: 'type2' },
        { key: 'key3', value: 'value3', type: 'type3' },
        { key: 'key4', value: 'value4', type: 'type1' },
    ],
    name1: 'name',
    switch: true,
    datePicker: '2020-06-11T14:00:00.000Z',
    timePicker: '2020-06-11T14:00:00.000Z',
    confirm: true,
    table: [
        { id: 'id0000012', name: 'Engagement 12', createdDate: '2019-11-12' },
        { id: 'id0000013', name: 'Engagement 13', createdDate: '2020-01-01' },
    ],
};

<FormRenderer
    schema={schema}
    customComponentWrapper={customComponentMapping}
    initialValues={initialValues}
    onSubmit={console.log}
    onCancel={console.log}
/>
```

```jsx
import FormRenderer, { componentTypes } from 'aws-northstar/components/FormRenderer';
import Container from 'aws-northstar/layouts/Container';
import Box from 'aws-northstar/layouts/Box';
import Input from 'aws-northstar/components/Input';
import Text from 'aws-northstar/components/Text';

const CustomComponentSimple = ({ label }) => <Text>{label}</Text>;

const CustomComponentComplex = ({ input }) => <Input 
    onChange={input.onChange} 
    value={input.value}/>

const schema = {
    fields: [
        {
            component: componentTypes.CUSTOM,
            name: 'text',
            label: 'This is the content of custom component',
            CustomComponent: CustomComponentSimple,
        },
        {
            component: componentTypes.CUSTOM,
            name: 'input',
            CustomComponent: CustomComponentComplex,
        },
    ],
    header: 'Data driven form with Custom Component',
    description:
        'Custom Component is an extention of Review Component which allows users to include custom business logic',
};

<Container>
    <FormRenderer 
        schema={schema} 
        initialValues={{
            input: 'initial input'
        }}
        onSubmit={console.log} 
        onCancel={console.log} />
</Container>
```

```jsx
import { useCallback } from 'react';
import FormRenderer, { componentTypes } from 'aws-northstar/components/FormRenderer';
import Container from 'aws-northstar/layouts/Container';
import FileUpload from 'aws-northstar/components/FileUpload';

const FileUploadComponent = ({ name, input, onChange }) => {
   const handleOnChange = useCallback(files => {
            if(files && files.length > 0) {
                if(onChange) {
                    onChange(files);
                }
    
                input.onChange(files.map(f => f.name));
            }
       },
       [input, onChange]
   );
   return <FileUpload controlId={name} onChange={handleOnChange} />
}

const schema = {
    fields: [
        {
            component: componentTypes.CUSTOM,
            name: 'file',
            CustomComponent: FileUploadComponent,
            onChange: console.log
        },
    ],
    header: 'Data driven form using FileUpload',
    description:
        'File upload logic can be implemented outside FormRenderer',
};

<FormRenderer 
    schema={schema} 
    onSubmit={console.log} 
    onCancel={console.log} />;

```

```jsx
import { useCallback } from 'react';
import FormRenderer, { componentTypes } from 'aws-northstar/components/FormRenderer';
import Container from 'aws-northstar/layouts/Container';

const schema = {
    fields: [
        {
            component: componentTypes.TEXT_FIELD,
            name: 'input',
            isDisabled: true,
        },
    ],
    header: 'Spinner while submitting',
};

<Container>
    <FormRenderer schema={schema} onSubmit={console.log} onCancel={console.log} isSubmitting={true} />
</Container>
```

```jsx
import Container from 'aws-northstar/layouts/Container';
import FormRenderer, { componentTypes, validatorTypes } from 'aws-northstar/components/FormRenderer';
import FormRendererMarkdownEditor from 'aws-northstar/components/FormRendererMarkdownEditor';

const customComponentMapping = {
    "MARKDOWN_EDITOR": FormRendererMarkdownEditor
}

const schema = {
    submitLabel: 'Save',
    cancelLabel: 'Back',
    fields: [
        {
            component: 'MARKDOWN_EDITOR',
            name: 'markdownOne',
            label: 'This is a markdown editor',
            helperText: 'Helper text provides users some guidance.',
            initialValue: '# I am a Markdown editor.\n\rHave a play.',
            onChange: console.log,
            validate: [
                {
                    type: validatorTypes.REQUIRED,
                },
            ],
        },
        {
            component: 'MARKDOWN_EDITOR',
            name: 'markdownTwo',
            label: 'This is a read only markdown editor',
            isReadOnly: true,
            initialValue: '# I should be read only\n\rAnd you should not be able to edit me',
        },
    ],
    header: 'Markdown Editor',
    description: 'This component allows a user to enter markdown and renders it in real-time.',
};

<Container>
    <FormRenderer 
        schema={schema} 
        customComponentWrapper={customComponentMapping}
        onSubmit={console.log} 
        onCancel={console.log} />
</Container>
    
```

```jsx
import FormRenderer, { componentTypes, validatorTypes } from 'aws-northstar/components/FormRenderer';
import Container from 'aws-northstar/layouts/Container';

const controlInteractionSchema = {
    fields: [
        {
            component: componentTypes.SELECT,
            name: 'select1',
            label: 'Select 1',
            placeholder: 'Choose an option',
            options: [
                {
                    label: 'Option 1',
                    value: '1',
                },
                {
                    label: 'Option 2',
                    value: '2',
                },
                {
                    label: 'Option 3',
                    value: '3',
                },
            ],
            isRequired: true,
            validate: [
                {
                    type: validatorTypes.REQUIRED,
                },
            ],
        },
        {
            component: componentTypes.SELECT,
            name: 'select2',
            label: 'Select 2',
            helperText: 'Enabled only when the value of Select 1 is 2 and default value changes with the value of select1',
            placeholder: 'Choose an option',
            options: [
                {
                    label: 'Option 21',
                    value: '21',
                },
                {
                    label: 'Option 22',
                    value: '22',
                },
                {
                    label: 'Option 23',
                    value: '23',
                },
            ],
            isRequired: true,
            validate: [
                {
                    type: validatorTypes.REQUIRED,
                },
            ],
            resolveProps: (_props, _field, formOptions) => {
                const values = formOptions.getState().values;
                return values.select1 === '2'
                    ? {
                          isDisabled: false,
                      }
                    : {
                          isDisabled: true,
                      };
            },
            condition: {
                when: 'select1',
                is: '2',
                then: { visible: true, set: { select2: '22' } },
                else: { visible: true, set: { select2: '21' } },
            },
        },
        {
            component: componentTypes.SELECT,
            name: 'select3',
            label: 'Select 3',
            helperText: 'Options changes with the value of Select 1 and only visible when Select 1 is set',
            placeholder: 'Choose an option',
            resolveProps: (_props, _field, formOptions) => {
                const values = formOptions.getState().values;
                return {
                    options: [
                        {
                            label: `Option 3${values.select1}1`,
                            value: `3${values.select1}1`,
                        },
                        {
                            label: `Option 3${values.select1}2`,
                            value: `3${values.select1}2`,
                        },
                        {
                            label: `Option 3${values.select1}3`,
                            value: `3${values.select1}3`,
                        },
                    ],
                };
            },
            condition: {
                when: 'select1',
                isNotEmpty: true,
            },
        },
    ],
    header: 'Control Interaction'
};

<Container>
    <FormRenderer
        schema={controlInteractionSchema}
        onSubmit={console.log}
        onCancel={console.log}
        subscription={{ values: true }}
    />
</Container>

```