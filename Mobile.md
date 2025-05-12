```tsx
1. CardPrato.tsx

const CardPrato = ({ nome, calorias, preco, imagem, onPress }) => {
  return (
    <TouchableOpacity onPress={onPress} style={styles.card}>
      <Image source={imagem} style={styles.imagem} />
      <View style={styles.info}>
        <Text style={styles.nome}>{nome}</Text>
        <Text style={styles.calorias}>{calorias} Calorias</Text>
        <Text style={styles.preco}>R$ {preco}</Text>
      </View>
    </TouchableOpacity>
  );
};


2. HomeScreen.tsx

const HomeScreen = () => {
  const navigation = useNavigation();

  const pratos = [
    { nome: 'Beef Burger', calorias: 70, preco: 12.0, imagem: require('../assets/images/beef_burger.png') },
    { nome: 'Pancakes', calorias: 60, preco: 15.0, imagem: require('../assets/images/pancakes.png') },
    { nome: 'Salad', calorias: 30, preco: 10.0, imagem: require('../assets/images/salad.png') },
    { nome: 'Spaghetti', calorias: 80, preco: 20.0, imagem: require('../assets/images/spaghetti.png') },
  ];

  return (
    <ScrollView contentContainerStyle={styles.container}>
      <Text style={styles.titulo}>Pratos</Text>
      {pratos.map((prato, index) => (
        <CardPrato
          key={index}
          nome={prato.nome}
          calorias={prato.calorias}
          preco={prato.preco}
          imagem={prato.imagem}
          onPress={() => navigation.navigate('Detalhes', { prato })}
        />
      ))}
    </ScrollView>
  );
};

3. DetalhesScreen.tsx 

const DetalhesScreen = ({ route }) => {
  const { prato } = route.params;
  const [quantidade, setQuantidade] = useState(1);

  const aumentar = () => setQuantidade(quantidade + 1);
  const diminuir = () => {
    if (quantidade > 1) setQuantidade(quantidade - 1);
  };

  return (
    <ScrollView style={styles.container}>
      <Text style={styles.titulo}>{prato.nome}</Text>
      <Image source={prato.imagem} style={styles.imagem} />
      <View style={styles.controles}>
        <TouchableOpacity onPress={diminuir}><Text style={styles.botao}>-</Text></TouchableOpacity>
        <Text style={styles.quantidade}>{quantidade}</Text>
        <TouchableOpacity onPress={aumentar}><Text style={styles.botao}>+</Text></TouchableOpacity>
      </View>
      <Text style={styles.preco}>R$ {(prato.preco * quantidade).toFixed(2)}</Text>
      <View style={styles.info}>
        <Text style={styles.infoItem}>⭐ 4.9</Text>
        <Text style={styles.infoItem}>{prato.calorias} Calorias</Text>
        <Text style={styles.infoItem}>20-30 Min</Text>
      </View>
      <Text style={styles.descricao}>Descrição do prato. Receita tradicional e muito saborosa.</Text>
      <View style={styles.botoes}>
        <TouchableOpacity style={styles.btnSec}><Text style={styles.btnTexto}>Add To Cart</Text></TouchableOpacity>
        <TouchableOpacity style={styles.btnPrim}><Text style={styles.btnTexto}>Buy Now</Text></TouchableOpacity>
      </View>
    </ScrollView>
  );
};
