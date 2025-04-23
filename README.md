import React, { useState } from 'react'; import { View, Text, TextInput, Button, ScrollView } from 'react-native';

export default function App() { const [weight, setWeight] = useState(''); const [milk, setMilk] = useState(''); const [fat, setFat] = useState(''); const [result, setResult] = useState(null);

const calculateNeeds = () => { const W = parseFloat(weight); const M = parseFloat(milk); const F = parseFloat(fat);

if (!W || !M || !F) return;

const maintenanceEnergy = 0.08 * W;
const milkEnergy = M * (0.0929 * F + 0.2057);
const totalME = maintenanceEnergy + milkEnergy;
const crudeProtein = 0.456 * M + 0.01 * W;

setResult({
  totalME: totalME.toFixed(2),
  crudeProtein: crudeProtein.toFixed(2),
});

};

return ( <ScrollView contentContainerStyle={{ padding: 20 }}> <Text style={{ fontSize: 24, fontWeight: 'bold', marginBottom: 20 }}> العلائق الذكية - NRC </Text>

<Text>وزن الحيوان (كجم):</Text>
  <TextInput
    keyboardType="numeric"
    value={weight}
    onChangeText={setWeight}
    style={{ borderWidth: 1, marginBottom: 10, padding: 8 }}
  />

  <Text>إنتاج الحليب (كجم/يوم):</Text>
  <TextInput
    keyboardType="numeric"
    value={milk}
    onChangeText={setMilk}
    style={{ borderWidth: 1, marginBottom: 10, padding: 8 }}
  />

  <Text>نسبة دهن الحليب (%):</Text>
  <TextInput
    keyboardType="numeric"
    value={fat}
    onChangeText={setFat}
    style={{ borderWidth: 1, marginBottom: 10, padding: 8 }}
  />

  <Button title="احسب الاحتياجات" onPress={calculateNeeds} />

  {result && (
    <View style={{ marginTop: 20 }}>
      <Text style={{ fontSize: 18 }}>
        الطاقة الصافية (Mcal): {result.totalME}
      </Text>
      <Text style={{ fontSize: 18 }}>
        البروتين الخام المطلوب (جم): {result.crudeProtein}
      </Text>
    </View>
  )}
</ScrollView>

); }

