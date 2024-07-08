Biblioteca muito útil para trabalhar com dropdowns!

```jsx
npm install react-native-select-dropdown
```

Sua utilização é extremamente simples:

```jsx
<SelectDropdown data={filterOption}
                buttonStyle={{backgroundColor: 'transparent'}}
                buttonTextStyle={{color: 'white'}}
                dropdownStyle={{backgroundColor:'white', borderRadius: 6}}
                onSelect={(selected)=> console.log(selected)}
                defaultButtonText={'Sem Filtro.'}
                renderDropdownIcon={()=> <FunnelSimple size={32} color={'white'}/>}
```


Subtópico: [[Bibliotecas RN]]