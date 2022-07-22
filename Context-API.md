## Context API

Context API fornece um meio de passar dados através da árvore de componentes sem a necessidade de passar props manualmente em cada nível. Para criar um contexto, utiliza-se o método createContext do React.

```
import React, { createContext } from 'react';

const MyContext = createContext(defaultValue);
```