import React, { useState } from 'react';
import { View, TextInput, Button, Alert, Image } from 'react-native';

const IMCCalculator = () => {
  const [weight, setWeight] = useState('');
  const [height, setHeight] = useState('');
  const [imcResult, setImcResult] = useState(null);

  const calculateIMC = () => {
    const weightValue = parseFloat(weight);
    const heightValue = parseFloat(height);
    const imc = weightValue / (heightValue * heightValue);

    let status = '';
    if (imc < 18.5) {
      status = 'Abaixo do Peso';
    } else if (imc < 25) {
      status = 'Peso Normal';
    } else if (imc < 30) {
      status = 'Sobrepeso';
    } else if (imc < 35) {
      status = 'Obesidade Grau I';
    } else if (imc < 40) {
      status = 'Obesidade Grau II';
    } else {
      status = 'Obesidade Mórbida';
    }

    setImcResult({ value: imc, status });
    Alert.alert('IMC Result', `Seu IMC é ${imc.toFixed(2)} - ${status}`);
  };

  return (
    <View>
      <TextInput
        placeholder="Peso (kg)"
        value={weight}
        onChangeText={(text) => setWeight(text)}
        keyboardType="numeric"
      />
      <TextInput
        placeholder="Altura (m)"
        value={height}
        onChangeText={(text) => setHeight(text)}
        keyboardType="numeric"
      />
      <Button title="Calcular IMC" onPress={calculateIMC} />
      {imcResult && (
        <>
          <Text>IMC: {imcResult.value.toFixed(2)}</Text>
          <Text>Status: {imcResult.status}</Text>
          {/* Adicione a lógica para exibir a imagem correspondente ao status do IMC */}
          <Image source={/* Path da imagem correspondente ao status */} />
        </>
      )}
    </View>
  );
};

export default IMCCalculator;
