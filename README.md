# UKM Vue Komponenter

Forskjellige Vue komponenter som brukes på ulike UKM systemer hvor Vue brukes

## For å hente pakken bruk npm
https://www.npmjs.com/package/ukm-vue-komponenter

```nodejs
npm i ukm-vue-komponenter
```

## Generelt
Hvordan oppretter man en komponent?

```vue
<template>
  <div>
    <table-komponent :loading="loading" :keys="[]" :values="[]"></table-komponent>
  </div>
</template>
```

```typescript
import TableKomponent from 'ukm-vue-komponenter';

class MyClass extends Vue {
    public loading = false;
    public components = [TableKomponent];
    ...
```

## Komponenter
### TableKomponent
Argumenter som må sendes:
```typescript
@Prop() keys!: {navn : string, method : string}[];
@Prop() values!: any[];
@Prop() loading!: boolean;
```

- **keys** aksepterer en liste med objekter som implementerer {navn : string, method : string}. Det betyr at navn er **key** og method er **verdien** som skal returneres når metode kalles i klassen.
- **values** aksepterer en liste med objekter hvor methods fra keys (keys.methods) kan kalles for å hente data
- **loading** aksepterer en boolean som indikerer om loading skal vises eller ikke

For eksempel:
```typescript
values = [ClassItem, ClassItem];
keys = classItem.getKeysForTable();
```

Klasse TableItem:
```typescript
class TableItem {
    private sporsmaal : string;

    public getSporsmaal() : string {
        return this.sporsmaal;
    }

    public getKeysForTable() : {navn : string, method : string}[] {
        return [
            {navn : 'Spørsmål', method :'getSporsmaal'}
        ];
    }
}
```
#### Resultatet fra eksempelet:
<img width="227" alt="Skjermbilde 2022-12-13 kl  18 53 45" src="https://user-images.githubusercontent.com/10181004/207408459-ee11bb0b-acea-410a-bdab-e58ee02356df.png">


### Andre funksjoner
I tillegg har TableKomponent metode for å sortere, fjerne og legge til igjen keys.
