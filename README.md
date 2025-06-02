

VeterinariaApp/
├── App.js
├── components/
│   └── AnamnesisForm.js
├── utils/
│   └── questions.js
└── package.json




{
  "name": "VeterinariaApp",
  "version": "1.0.0",
  "main": "node_modules/expo/AppEntry.js",
  "scripts": {
    "start": "expo start"
  },
  "dependencies": {
    "expo": "~50.0.0",
    "react": "18.2.0",
    
    "react-native": "0.73.0"
  }
}



import React from 'react';
import { SafeAreaView, StyleSheet, Text } from 'react-native';
import AnamnesisForm from './components/AnamnesisForm';

export default function App() {
  return (
    <SafeAreaView style={styles.container}>
      <Text style={styles.title}>Anamnese Veterinária</Text>
      <AnamnesisForm />
    </SafeAreaView>
  
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 20,
    marginTop: 40,
    backgroundColor: '#f2f2f2'
  },
  title: {
    fontSize: 24,
    fontWeight: 'bold',
    marginBottom: 20,
  },
});


---

🧾 components/AnamnesisForm.js

import React, { useState } from 'react';
import { View, Text, TextInput, Button, StyleSheet, ScrollView, Alert } from 'react-native';
import questions from '../utils/questions';

export default function AnamnesisForm() {
  const [answers, setAnswers] = useState({});

  const handleChange = (key, value) => {
    setAnswers({ ...answers, [key]: value });
  };

  const handleSubmit = () => {
    console.log("Respostas:", answers);
    Alert.alert('Formulário Enviado', 'As respostas foram registradas com sucesso!');
    // Aqui você pode enviar para backend ou salvar localmente
  };

  return (
    <ScrollView>
      {questions.map((q, index) => (
        <View key={index} style={styles.questionContainer}>
          <Text style={styles.question}>{q.label}</Text>
          <TextInput
            style={styles.input}
            placeholder="Digite aqui..."
            onChangeText={(text) => handleChange(q.key, text)}
            multiline
          />
        </View>
      ))}
      <Button title="Enviar" onPress={handleSubmit} />
    </ScrollView>
  );
}

const styles = StyleSheet.create({
  questionContainer: {
    marginBottom: 15,
  },
  question: {
    fontSize: 16,
    fontWeight: '500',
  },
  input: {
    backgroundColor: '#fff',
    padding: 10,
    borderRadius: 8,
    marginTop: 5,
    borderWidth: 1,
    borderColor: '#ccc',
  },
});

export default [
  { key: 'owner_name', label: 'Nome do tutor:' },
  { key: 'animal_name', label: 'Nome do animal:' },
  { key: 'species', label: 'Espécie (cão, gato, etc.):' },
  { key: 'breed', label: 'Raça:' },
  { key: 'age', label: 'Idade aproximada:' },
  { key: 'sex', label: 'Sexo do animal:' },
  { key: 'problem_duration', label: 'Há quanto tempo o problema começou?' },
  { key: 'symptoms', label: 'Quais os sintomas observados?' },
  { key: 'feeding', label: 'Como é a alimentação do animal?' },
  { key: 'vaccination', label: 'Vacinas em dia?' },
  { key: 'deworming', label: 'Vermifugação atualizada?' },
  { key: 'other_info', label: 'Outras informações importantes:' },
];


