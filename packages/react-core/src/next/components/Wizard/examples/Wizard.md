---
id: Wizard
section: components
cssPrefix: pf-c-wizard
propComponents:
  [
    'Wizard',
    'WizardFooter',
    'WizardToggle',
    'WizardStep',
    'WizardBody',
    'WizardHeader',
    'WizardNav',
    'WizardNavItem',
    'WizardContextProps',
    'WizardBasicStep',
    'WizardParentStep',
    'WizardSubStep',
    'DefaultWizardNavProps',
    'DefaultWizardFooterProps',
  ]
beta: true
---

import {
FormGroup,
TextInput,
Drawer,
DrawerContent,
Button,
Flex,
DrawerPanelContent,
DrawerColorVariant,
DrawerHead,
DrawerActions,
DrawerCloseButton
} from '@patternfly/react-core';
import {
Wizard,
WizardFooter,
WizardToggle,
WizardStep,
WizardBody,
useWizardFooter,
useWizardContext,
WizardNavItem,
WizardNav,
WizardHeader
} from '@patternfly/react-core/next';
import { css } from '@patternfly/react-styles';
import styles from '@patternfly/react-styles/css/components/Wizard/wizard';

PatternFly has two implementations of a `Wizard`. This newer `Wizard` takes a more explicit and declarative approach compared to the older implementation, which can be found under the [React](/components/wizard/react) tab.

## Examples

### Basic

```ts file="./WizardBasic.tsx"
```

### Custom navigation

The `Wizard`'s `nav` property can be used to build your own navigation.

```
/** Callback for the Wizard's 'nav' property. Returns element which replaces the Wizard's default navigation. */
export type CustomWizardNavFunction = (
  isOpen: boolean,
  steps: WizardControlStep[],
  activeStep: WizardControlStep,
  goToStepByIndex: (index: number) => void
) => React.ReactElement<WizardNavProps>;

/** Encompasses all step type variants that are internally controlled by the Wizard */
type WizardControlStep = WizardBasicStep | WizardParentStep | WizardSubStep;
```

```ts file="./WizardCustomNav.tsx"
```

### Kitchen sink

Includes a header, custom footer, sub-steps, step content with a drawer, custom nav item, and nav prevention until step visitation.

Custom operations when navigating between steps can be achieved by utilizing `onNext`, `onBack` or `onNavByIndex` properties whose callback functions return the 'id' and 'name' of the currently focused step (currentStep), and the previously focused step (previousStep).

```
/** Callback for the Wizard's 'onNext', 'onBack', and 'onNavByIndex' properties */
type WizardNavStepFunction = (currentStep: WizardNavStepData, previousStep: WizardNavStepData) => void;

/** Data returned for either parameter of WizardNavStepFunction */
type WizardNavStepData = Pick<WizardControlStep, 'id' | 'name'>;
```

```ts file="./WizardKitchenSink.tsx"
```

## Hooks

### useWizardFooter

Used to set a unique footer for the wizard on any given step. See step 3 of [Kitchen sink](#kitchen-sink) for a live example.

```noLive
import { useWizardFooter } from '@patternfly/react-core/next';

const StepContent = () => {
  useWizardFooter(<>Some footer</>);
  return <>Step content</>;
}
```

### useWizardContext

Used to access any property of [WizardContext](#wizardcontextprops):

```noLive
import { useWizardContext } from '@patternfly/react-core/next';

const StepContent = () => {
  const { activeStep } = useWizardContext();
  return <>This is the active step: {activeStep}</>;
}
```