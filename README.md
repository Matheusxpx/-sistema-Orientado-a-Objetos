# -sistema-Orientado-a-Objetos
MATHEUS LUCAS DE SOUZA PEREIRA: 326142119 
meu codigo completo CLASSE CARTA <img width="1911" height="1000" alt="image" src="https://github.com/user-attachments/assets/3c060543-eea0-44bd-8534-314455bd9aa0" />]
CLASSE GERENCIADOR DE FINANCEIRO   <img width="1297" height="781" alt="image" src="https://github.com/user-attachments/assets/b3507edd-3ec7-4547-9ecb-3682ff342789" />
CLASSE TELACADASTRO <img width="1241" height="823" alt="image" src="https://github.com/user-attachments/assets/eefdc847-28d1-4432-b2c7-e9b624e608e8" />
CLASSE TELACADASTR <img width="1135" height="878" alt="image" src="https://github.com/user-attachments/assets/45792888-db64-4884-8b31-e56e65062b78" />
CLASSE TELACADASTR <img width="1060" height="721" alt="image" src="https://github.com/user-attachments/assets/c48e0bcd-8156-4422-84ca-82df9fefb1e1" />
CLASSE TELA LOGIN <img width="1853" height="882" alt="image" src="https://github.com/user-attachments/assets/128c9e68-d301-4e1e-9d5c-4b5abf126ea5" />
CLASSE TORNEIO <img width="1128" height="806" alt="image" src="https://github.com/user-attachments/assets/325d7604-0f2a-44db-8fd0-3dacf82f6804" />
CLASSE TORNEIO <img width="1171" height="626" alt="image" src="https://github.com/user-attachments/assets/6524a018-a6cf-4a6c-aa9a-799cb7ae4859" />
CLASSE TREINADOR <img width="1222" height="700" alt="image" src="https://github.com/user-attachments/assets/c6767070-9dc5-42d4-a541-c08b39653655" />
MAIN SISTEMA <img width="1252" height="720" alt="image" src="https://github.com/user-attachments/assets/fca96e2c-7bc2-475f-9158-e9b2975d4a20" />
CLASSE LOJA <img width="1050" height="545" alt="image" src="https://github.com/user-attachments/assets/62a11d1e-c9c0-4350-be0c-53a7b9c2e97e" />
TELA JOGO PRINCIPAL /*
 * Click nbfs://nbhost/SystemFileSystem/Templates/Licenses/license-default.txt to change this license
 * Click nbfs://nbhost/SystemFileSystem/Templates/Classes/Class.java to edit this template
 */
package sistemayugioh;

/**
 *
 * @author unite
 */

import javax.swing.*;
import javax.swing.table.DefaultTableModel;
import javax.swing.filechooser.FileNameExtensionFilter;
import java.awt.*;
import java.awt.event.MouseAdapter;
import java.awt.event.MouseEvent;
import java.io.File;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.InputStream;
import java.net.URL;
import java.net.HttpURLConnection;
import java.util.ArrayList;
import java.util.Collections;
import java.util.Random;

public class TelaJogoPrincipal extends JFrame { 
    private String jogadorLogado;
    private double caixaLoja = 1000.00;
    private Treinador treinador;
    private ArrayList<String> cartasNome = new ArrayList<>();
    private ArrayList<Integer> cartasAtk = new ArrayList<>();
    private ArrayList<Integer> cartasDef = new ArrayList<>(); 
    private ArrayList<Integer> cartasNivel = new ArrayList<>(); 
    private ArrayList<String> cartasImagem = new ArrayList<>(); 

    private JPanel painelDeckVisual; 
    private JLabel lblInfo;

    public TelaJogoPrincipal(String jogador) {
        this.jogadorLogado = jogador;
        this.treinador = new Treinador(jogador, 500.00);
        
       
        cartasNome.add("Mago Negro"); cartasAtk.add(2500); cartasDef.add(2100); cartasNivel.add(7); cartasImagem.add("Mago Negro.Png"); 
        cartasNome.add("Dragão Branco de Olhos Azuis"); cartasAtk.add(3000); cartasDef.add(2500); cartasNivel.add(8); cartasImagem.add("Dragão Branco de Olhos Azuis.png"); 

        
        cartasNome.add("Exodia, o Proibido"); cartasAtk.add(4000); cartasDef.add(4000); cartasNivel.add(10); cartasImagem.add("Exodia.png");
        cartasNome.add("Obelisco, o Atormentador"); cartasAtk.add(4000); cartasDef.add(4000); cartasNivel.add(10); cartasImagem.add("Obelisco.png");
        cartasNome.add("Slifer, o Dragão dos Céus"); cartasAtk.add(3500); cartasDef.add(3500); cartasNivel.add(10); cartasImagem.add("Slifer.png");
        cartasNome.add("Dragão Alado de Rá"); cartasAtk.add(4500); cartasDef.add(4500); cartasNivel.add(10); cartasImagem.add("Ra.png");

        setTitle("Arena Yu-Gi-Oh! - Painel Principal com Sistema de Torneio");
        setSize(1050, 650); 
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLocationRelativeTo(null);
        getContentPane().setBackground(new Color(20, 15, 25));
        setLayout(new BorderLayout(10, 10));

        lblInfo = new JLabel(
"Duelista: " + jogadorLogado +
" | Saldo: R$ " + treinador.getSaldo(),
SwingConstants.CENTER
);
        lblInfo.setFont(new Font("Arial", Font.BOLD, 14));
        lblInfo.setForeground(Color.WHITE);
        lblInfo.setOpaque(true);
        lblInfo.setBackground(new Color(35, 140, 35)); 
        lblInfo.setPreferredSize(new Dimension(850, 40));
        add(lblInfo, BorderLayout.NORTH);

        painelDeckVisual = new JPanel();
        painelDeckVisual.setBackground(new Color(15, 10, 20));
        painelDeckVisual.setLayout(new FlowLayout(FlowLayout.LEFT, 15, 15));
        
        JScrollPane scrollDeck = new JScrollPane(painelDeckVisual);
        scrollDeck.setBorder(BorderFactory.createEmptyBorder());
        scrollDeck.setViewportBorder(BorderFactory.createEmptyBorder());
        
        JLabel lblTituloDeck = new JLabel("  DECK DE CARTAS VISUAL (Clique na carta para Detalhes)");
        lblTituloDeck.setFont(new Font("Arial", Font.BOLD, 14));
        lblTituloDeck.setForeground(new Color(50, 205, 50));
        lblTituloDeck.setBorder(BorderFactory.createEmptyBorder(10, 5, 5, 5));

        JPanel painelCentralContenedor = new JPanel(new BorderLayout());
        painelCentralContenedor.setBackground(new Color(20, 15, 25));
        painelCentralContenedor.add(lblTituloDeck, BorderLayout.NORTH);
        painelCentralContenedor.add(scrollDeck, BorderLayout.CENTER);
        
        add(painelCentralContenedor, BorderLayout.CENTER);

        JPanel painelBotoes = new JPanel(new GridLayout(10, 1, 8, 8));
        painelBotoes.setBackground(new Color(20, 15, 25));
        painelBotoes.setBorder(BorderFactory.createEmptyBorder(10, 10, 10, 10));

        JButton btnListar = criarBotaoElegante(" Atualizar Deck");
        JButton btnCadastrar = criarBotaoElegante(" Cadastrar Carta (Criar Altos ATK)");
        JButton btnEditarDeck = criarBotaoElegante(" Gerenciar e Editar Deck"); 
        JButton btnExcluir = criarBotaoElegante(" Remover Carta (D)");
        JButton btnServico = criarBotaoElegante("� ENTRAR EM DUELO (ARENA) "); 
        JButton btnJogar = criarBotaoElegante(" SIMULAR TORNEIO (MATA-MATA)");
        JButton btnLoja = criarBotaoElegante("� LOJINHA DE CARTAS");

        painelBotoes.add(btnListar); 
        painelBotoes.add(btnCadastrar);
        painelBotoes.add(btnEditarDeck); 
        painelBotoes.add(btnExcluir); 
        painelBotoes.add(btnServico);
        painelBotoes.add(btnJogar);
        painelBotoes.add(btnLoja);
        
        add(painelBotoes, BorderLayout.WEST);

        btnListar.addActionListener(e -> renderizarDeck());
        

        btnCadastrar.addActionListener(e -> {
            String nome = JOptionPane.showInputDialog(this, "Carta Nova:");
            if (nome != null && !nome.trim().isEmpty()) {
                String atkStr = JOptionPane.showInputDialog(this, "Pontos de ATK (Dica: coloque > 3000 para vencer):");
                String defStr = JOptionPane.showInputDialog(this, "Pontos de DEF:");
                String nivelStr = JOptionPane.showInputDialog(this, "Nível da Carta (1 a 12):");
                
                try {
                    int atk = Integer.parseInt(atkStr);
                    int def = Integer.parseInt(defStr);
                    int nivel = Integer.parseInt(nivelStr);
                    if (nivel < 1 || nivel > 12) nivel = 4; 
                    
                    String nomeArquivoFinal = "default.jpg";

                    String[] opcoesOrigem = {"Escolher arquivo do PC", "Inserir Link HTTP"};
                    int escolhaOrigem = JOptionPane.showOptionDialog(this, "Como deseja enviar a imagem?", "Imagem", 
                            JOptionPane.DEFAULT_OPTION, JOptionPane.QUESTION_MESSAGE, null, opcoesOrigem, opcoesOrigem[0]);

                    if (escolhaOrigem == 0) {
                        JFileChooser buscadorArquivos = new JFileChooser();
                        buscadorArquivos.setFileFilter(new FileNameExtensionFilter("Imagens", "png", "jpg", "jpeg"));
                        if (buscadorArquivos.showOpenDialog(this) == JFileChooser.APPROVE_OPTION) {
                            File arquivoSelecionado = buscadorArquivos.getSelectedFile();
                            nomeArquivoFinal = nome.replaceAll("[^a-zA-Z0-9]", "_") + ".png";
                            copiarArquivoLocal(arquivoSelecionado, new File("src/sistemayugioh/Imagem/" + nomeArquivoFinal));
                        }
                    } else if (escolhaOrigem == 1) {
                        String urlInternet = JOptionPane.showInputDialog(this, "Insira a URL completa:");
                        if (urlInternet != null && !urlInternet.trim().isEmpty()) {
                            nomeArquivoFinal = nome.replaceAll("[^a-zA-Z0-9]", "_") + ".png";
                            baixarImagemWeb(urlInternet.trim(), "src/sistemayugioh/Imagem/" + nomeArquivoFinal);
                        }
                    }

                    cartasNome.add(nome);
                    cartasAtk.add(atk);
                    cartasDef.add(def);
                    cartasNivel.add(nivel);
                    cartasImagem.add(nomeArquivoFinal);
                    renderizarDeck();
                } catch (NumberFormatException ex) {
                    JOptionPane.showMessageDialog(this, "Valores numéricos inválidos.");
                }
            }
        });

        btnEditarDeck.addActionListener(e -> abrirJanelaGerenciarDeck());
        btnLoja.addActionListener(e -> abrirLoja()); 

        btnExcluir.addActionListener(e -> {
            if (cartasNome.isEmpty()) return;
            String[] nomes = cartasNome.toArray(new String[0]);
            String escolhida = (String) JOptionPane.showInputDialog(this, "Selecione:", "Excluir", JOptionPane.QUESTION_MESSAGE, null, nomes, nomes[0]);
            if (escolhida != null) {
                int idx = cartasNome.indexOf(escolhida);
                cartasNome.remove(idx); cartasAtk.remove(idx); cartasDef.remove(idx); cartasNivel.remove(idx); cartasImagem.remove(idx);
                renderizarDeck();
            }
        });

        btnServico.addActionListener(e -> {
            if (cartasNome.isEmpty()) {
                JOptionPane.showMessageDialog(this, "Adicione cartas ao seu deck antes de duelar!");
                return;
            }
            abrirMesaDeDueloGrafica();
        });

        btnJogar.addActionListener(e -> {
            if (cartasNome.size() < 4) {
                JOptionPane.showMessageDialog(this, "Você precisa de pelo menos 4 cartas no deck para simular um torneio de chaves!");
                return;
            }

            ArrayList<Integer> indicesSorteados = new ArrayList<>();
            for (int i = 0; i < cartasNome.size(); i++) indicesSorteados.add(i);
            Collections.shuffle(indicesSorteados);

            while (indicesSorteados.size() < 8) {
                indicesSorteados.add(new Random().nextInt(cartasNome.size()));
            }

            int q1 = indicesSorteados.get(0); int q2 = indicesSorteados.get(1); 
            int q3 = indicesSorteados.get(2); int q4 = indicesSorteados.get(3); 
            int q5 = indicesSorteados.get(4); int q6 = indicesSorteados.get(5); 
            int q7 = indicesSorteados.get(6); int q8 = indicesSorteados.get(7); 

            String layoutQuartas = "\n" +
                                   "           TORNEIO MATA-MATA DA ARENA \n" +
                                   "\n\n" +
                                   " CONFRONTOS DAS QUARTAS DE FINAL:\n\n" +
                                   " [CHAVE A]: " + cartasNome.get(q1) + " (ATK:" + cartasAtk.get(q1) + ") VS " + cartasNome.get(q2) + " (ATK:" + cartasAtk.get(q2) + ")\n" +
                                   " [CHAVE B]: " + cartasNome.get(q3) + " (ATK:" + cartasAtk.get(q3) + ") VS " + cartasNome.get(q4) + " (ATK:" + cartasAtk.get(q4) + ")\n" +
                                   " [CHAVE C]: " + cartasNome.get(q5) + " (ATK:" + cartasAtk.get(q5) + ") VS " + cartasNome.get(q6) + " (ATK:" + cartasAtk.get(q6) + ")\n" +
                                   " [CHAVE D]: " + cartasNome.get(q7) + " (ATK:" + cartasAtk.get(q7) + ") VS " + cartasNome.get(q8) + " (ATK:" + cartasAtk.get(q8) + ")\n\n" +
                                   "Pressione OK para simular as Quartas e ir para a SEMIFINAL!";
            
            JOptionPane.showMessageDialog(this, layoutQuartas, "Chaves do Campeonato - Quartas", JOptionPane.INFORMATION_MESSAGE);

            int semi1 = (cartasAtk.get(q1) >= cartasAtk.get(q2)) ? q1 : q2;
            int semi2 = (cartasAtk.get(q3) >= cartasAtk.get(q4)) ? q3 : q4;
            int semi3 = (cartasAtk.get(q5) >= cartasAtk.get(q6)) ? q5 : q6;
            int semi4 = (cartasAtk.get(q7) >= cartasAtk.get(q8)) ? q7 : q8;

            String layoutSemi = "\n" +
                                "                 ETAPA: SEMIFINAL \n" +
                                "\n\n" +
                                "Vencedores das Quartas avançaram!\n\n" +
                                "  SEMI 1: " + cartasNome.get(semi1) + " VS " + cartasNome.get(semi2) + "\n" +
                                "  SEMI 2: " + cartasNome.get(semi3) + " VS " + cartasNome.get(semi4) + "\n\n" +
                                "Clique em OK para define os dois finalistas!";
            
            JOptionPane.showMessageDialog(this, layoutSemi, "Chaves do Torneio - Semifinal", JOptionPane.WARNING_MESSAGE);

            int finalista1 = (cartasAtk.get(semi1) >= cartasAtk.get(semi2)) ? semi1 : semi2;
            int finalista2 = (cartasAtk.get(semi3) >= cartasAtk.get(semi4)) ? semi3 : semi4;

            String layoutFinal = "\n" +
                                 "              A GRANDE FINAL DA ARENA \n" +
                                 "\n\n" +
                                 "  DISPUTA PELO TÍTULO:\n" +
                                 "  " + cartasNome.get(finalista1) + " (ATK " + cartasAtk.get(finalista1) + ")\n" +
                                 "        VS\n" +
                                 "  " + cartasNome.get(finalista2) + " (ATK " + cartasAtk.get(finalista2) + ")\n\n" +
                                 "Quem erguerá a taça? Clique para ver o resultado!";

            JOptionPane.showMessageDialog(this, layoutFinal, "Fase Final", JOptionPane.ERROR_MESSAGE);

           int campeaoIdx = (cartasAtk.get(finalista1) >= cartasAtk.get(finalista2))
        ? finalista1
        : finalista2;

double premio = 500.00;


treinador.adicionarSaldo(premio);


lblInfo.setText(
    "Duelista: " + jogadorLogado +
    " | Saldo: R$ " + treinador.getSaldo()
);

JOptionPane.showMessageDialog(
    this,
    "O CAMPEÃO SUPREMO DO TORNEIO É: "
    + cartasNome.get(campeaoIdx).toUpperCase()
    + "!!! \n\n"
    + " Prêmio recebido: R$ " + premio
    + "\n Novo saldo: R$ " + treinador.getSaldo()
    + "\n Nível: " + cartasNivel.get(campeaoIdx)
    + "\n Ataque: " + cartasAtk.get(campeaoIdx),
    "Pódio do Torneio",
    JOptionPane.INFORMATION_MESSAGE
);

}); 
    
renderizarDeck();
}
     private boolean copiarArquivoLocal(File orig, File dest) {
        try {
            dest.getParentFile().mkdirs();
            try (FileInputStream in = new FileInputStream(orig); FileOutputStream out = new FileOutputStream(dest)) {
                byte[] buf = new byte[4096]; int n;
                while ((n = in.read(buf)) > 0) out.write(buf, 0, n);
            }
            return true;
        } catch (Exception e) { return false; }
    }

    private void abrirJanelaGerenciarDeck() {
        JFrame frameEdicao = new JFrame("Gerenciador do Deck - Edição de Atributos");
        frameEdicao.setSize(650, 400);
        frameEdicao.setLocationRelativeTo(this);
        frameEdicao.getContentPane().setBackground(new Color(25, 20, 30));
        frameEdicao.setLayout(new BorderLayout());

        String[] colunas = {"Índice", "Nome", "ATK (Ataque)", "DEF (Defesa/Vida)", "Nível ⭐"};
        DefaultTableModel modelo = new DefaultTableModel(colunas, 0);
        for (int i = 0; i < cartasNome.size(); i++) {
            modelo.addRow(new Object[]{i, cartasNome.get(i), cartasAtk.get(i), cartasDef.get(i), cartasNivel.get(i)});
        }
        JTable tabela = new JTable(modelo);
        frameEdicao.add(new JScrollPane(tabela), BorderLayout.CENTER);

        JButton btnEd = new JButton(" Editar Totalmente a Carta Selecionada");
        btnEd.setBackground(new Color(35, 140, 35));
        btnEd.setForeground(Color.WHITE);
        btnEd.setFont(new Font("Arial", Font.BOLD, 13));
        
        btnEd.addActionListener(x -> {
            int r = tabela.getSelectedRow();
            if (r >= 0) {
                int idx = (int) tabela.getValueAt(r, 0);
                
                String nNome = JOptionPane.showInputDialog(frameEdicao, "Alterar Nome:", cartasNome.get(idx));
                String nAtkStr = JOptionPane.showInputDialog(frameEdicao, "Alterar ATK:", cartasAtk.get(idx));
                String nDefStr = JOptionPane.showInputDialog(frameEdicao, "Alterar DEF (Defesa/Vida):", cartasDef.get(idx));
                String nNivelStr = JOptionPane.showInputDialog(frameEdicao, "Alterar Nível (1 a 12):", cartasNivel.get(idx));
                
                if (nNome != null && nAtkStr != null && nDefStr != null && nNivelStr != null) {
                    try {
                        cartasNome.set(idx, nNome);
                        cartasAtk.set(idx, Integer.parseInt(nAtkStr));
                        cartasDef.set(idx, Integer.parseInt(nDefStr));
                        cartasNivel.set(idx, Integer.parseInt(nNivelStr));
                        
                        JOptionPane.showMessageDialog(frameEdicao, "Carta updated com sucesso!");
                        renderizarDeck();
                        frameEdicao.dispose();
                    } catch (NumberFormatException nex) {
                        JOptionPane.showMessageDialog(frameEdicao, "Erro: Insira apenas números válidos para ATK, DEF e Nível.");
                    }
                }
            } else {
                JOptionPane.showMessageDialog(frameEdicao, "Por favor, selecione uma linha da tabela primeiro!");
            }
        });
        
        frameEdicao.add(btnEd, BorderLayout.SOUTH);
        frameEdicao.setVisible(true);
    }

    private int meuLP = 8000;
    private int opositorLP = 8000;

    
    private void abrirMesaDeDueloGrafica() {
        String[] opcoesMinhas = cartasNome.toArray(new String[0]);
        String minhaEscolhida = (String) JOptionPane.showInputDialog(this, 
                "Escolha o Monstro do seu Deck para Invocar no Campo:", "Mesa de Invocação",
                JOptionPane.QUESTION_MESSAGE, null, opcoesMinhas, opcoesMinhas[0]);
        
        if (minhaEscolhida == null) return;
        int meuIdx = cartasNome.indexOf(minhaEscolhida);
        int meuAtaqueMesa = cartasAtk.get(meuIdx);
        int minhaDefesaMesa = cartasDef.get(meuIdx);
        String minhaImgMesa = cartasImagem.get(meuIdx);

        String[] inimigos = {"Seto Kaiba", "Yugi Muto", "Maximillion Pegasus", "Marik Ishtar"};
        String[] monstrosInimigos = {"Dragão Branco de Olhos Azuis", "Mago Negro", "Abandono", "Dragão Alado de Rá"};
        int[] atkInimigos = {3000, 2500, 0, 4000};
        int[] defInimigos = {2500, 2100, 0, 4000};
        
        Random r = new Random();
        int idxInimigo = r.nextInt(inimigos.length);
        String rival = inimigos[idxInimigo];
        String monstroRival = monstrosInimigos[idxInimigo];
        int atkRival = atkInimigos[idxInimigo];
        int defRival = defInimigos[idxInimigo];

        meuLP = 8000;
        opositorLP = 8000;

        JFrame janelaMesa = new JFrame("Mesa Oficial de Duelo - Yu-Gi-Oh! Arena");
        janelaMesa.setSize(950, 700);
        janelaMesa.setLocationRelativeTo(this);
        janelaMesa.setLayout(new BorderLayout());
        
        
        JPanel playmatTabuleiro = new JPanel(null) {
            @Override
            protected void paintComponent(Graphics g) {
                super.paintComponent(g);
               
                String caminhoFundo = "src/sistemayugioh/Imagem/fundo_atualizado.png";
                File arquivoFundo = new File(caminhoFundo);
                if (arquivoFundo.exists()) {
                    Image imgFundo = new ImageIcon(caminhoFundo).getImage();
                    g.drawImage(imgFundo, 0, 0, getWidth(), getHeight(), this);
                    
                    g.setColor(new Color(0, 0, 0, 150));
                    g.fillRect(0, 0, getWidth(), getHeight());
                } else {
                    g.setColor(new Color(20, 20, 22));
                    g.fillRect(0, 0, getWidth(), getHeight());
                }
            }
        };

        JLabel lblLpOpositor = new JLabel("Oponente:  " + rival + " | LP: " + opositorLP, SwingConstants.RIGHT);
        lblLpOpositor.setFont(new Font("Consolas", Font.BOLD, 20));
        lblLpOpositor.setForeground(new Color(255, 80, 80));
        lblLpOpositor.setBounds(450, 20, 430, 30);
        playmatTabuleiro.add(lblLpOpositor);

        JPanel zonaMonstroInimigo = new JPanel(new BorderLayout());
        zonaMonstroInimigo.setBounds(380, 80, 160, 180);
        zonaMonstroInimigo.setBackground(new Color(40, 20, 20, 210)); 
        zonaMonstroInimigo.setBorder(BorderFactory.createLineBorder(Color.RED, 2));
        
        JLabel lblImgInimigo = new JLabel();

String caminhoInimigo = "";

switch (idxInimigo) {
    case 0:
        caminhoInimigo = "src/sistemayugioh/Imagem/seto.png";
        break;
    case 1:
        caminhoInimigo = "src/sistemayugioh/Imagem/yugi.png";
        break;
    case 2:
        caminhoInimigo = "src/sistemayugioh/Imagem/pegasus.png";
        break;
    case 3:
        caminhoInimigo = "src/sistemayugioh/Imagem/marik.png";
        break;
}

if (new File(caminhoInimigo).exists()) {
    ImageIcon iconInimigo = new ImageIcon(caminhoInimigo);
    Image imgInimigo = iconInimigo.getImage().getScaledInstance(
            140,
            130,
            Image.SCALE_SMOOTH);

    lblImgInimigo.setIcon(new ImageIcon(imgInimigo));
} else {
    lblImgInimigo.setText("");
    lblImgInimigo.setFont(new Font("Arial", Font.BOLD, 48));
    lblImgInimigo.setHorizontalAlignment(SwingConstants.CENTER);
}
        JLabel lblTextoInimigo = new JLabel("<html><center>" + monstroRival + "<br><b>A:" + atkRival + " | D:" + defRival + "</b></center></html>", SwingConstants.CENTER);
        lblTextoInimigo.setForeground(Color.WHITE);
        zonaMonstroInimigo.add(lblImgInimigo, BorderLayout.CENTER);
        zonaMonstroInimigo.add(lblTextoInimigo, BorderLayout.SOUTH);
        playmatTabuleiro.add(zonaMonstroInimigo);

        JPanel barraFases = new JPanel(new FlowLayout(FlowLayout.CENTER, 25, 5));
        barraFases.setBackground(new Color(10, 25, 15, 230)); 
        barraFases.setBounds(180, 290, 580, 35);
        barraFases.setBorder(BorderFactory.createLineBorder(new Color(50, 205, 50)));
        
        String[] fasesArr = {"DP", "SP", "M1", "▶️ BP (BATTLE)", "M2", "EP"};
        for(String fName : fasesArr) {
            JLabel fLbl = new JLabel(fName);
            fLbl.setFont(new Font("Arial", Font.BOLD, 12));
            fLbl.setForeground(fName.contains("BP") ? Color.GREEN : Color.LIGHT_GRAY);
            barraFases.add(fLbl);
        }
        playmatTabuleiro.add(barraFases);

        JPanel zonaMeuMonstro = new JPanel(new BorderLayout());
        zonaMeuMonstro.setBounds(380, 350, 160, 180);
        zonaMeuMonstro.setBackground(new Color(20, 40, 25, 210)); 
        zonaMeuMonstro.setBorder(BorderFactory.createLineBorder(Color.GREEN, 2));
        
        JLabel lblMinhaImg = new JLabel();
        String pathMinha = "src/sistemayugioh/Imagem/" + minhaImgMesa;
        if(new File(pathMinha).exists()) {
            lblMinhaImg.setIcon(new ImageIcon(new ImageIcon(pathMinha).getImage().getScaledInstance(140, 130, Image.SCALE_SMOOTH)));
        } else {
            lblMinhaImg.setText("");
            lblMinhaImg.setFont(new Font("Arial", Font.BOLD, 48));
            lblMinhaImg.setHorizontalAlignment(SwingConstants.CENTER);
        }
        JLabel lblMeuTexto = new JLabel("<html><center>" + minhaEscolhida + "<br><b>A:" + meuAtaqueMesa + " | D:" + minhaDefesaMesa + "</b></center></html>", SwingConstants.CENTER);
        lblMeuTexto.setForeground(Color.WHITE);
        zonaMeuMonstro.add(lblMinhaImg, BorderLayout.CENTER);
        zonaMeuMonstro.add(lblMeuTexto, BorderLayout.SOUTH);
        playmatTabuleiro.add(zonaMeuMonstro);

        JLabel lblMeuLp = new JLabel(" " + jogadorLogado + " | LP: " + meuLP, SwingConstants.LEFT);
        lblMeuLp.setFont(new Font("Consolas", Font.BOLD, 20));
        lblMeuLp.setForeground(Color.GREEN);
        lblMeuLp.setBounds(30, 560, 400, 30);
        playmatTabuleiro.add(lblMeuLp);

        JButton btnAtacarMesa = new JButton("⚔️ SEU TURNO: DECLARAR ATAQUE (BATTLE PHASE) ⚔️");
        btnAtacarMesa.setBounds(460, 555, 430, 45);
        btnAtacarMesa.setBackground(new Color(34, 139, 34));
        btnAtacarMesa.setForeground(Color.WHITE);
        btnAtacarMesa.setFont(new Font("Arial", Font.BOLD, 12));
        
        btnAtacarMesa.addActionListener(act -> {
            if (meuLP <= 0 || opositorLP <= 0) return;

            JOptionPane.showMessageDialog(janelaMesa, "--- SEU TURNO ---\n" + minhaEscolhida + " (ATK " + meuAtaqueMesa + ") ataca o monstro " + monstroRival + " (DEF " + defRival + ")!");
            
            if (meuAtaqueMesa > defRival) {
                int diferenca = meuAtaqueMesa - defRival;
                opositorLP -= diferenca;
                JOptionPane.showMessageDialog(janelaMesa, "Sucesso! Você quebrou a defesa do inimigo. Ele perdeu " + diferenca + " de LP!");
            } else if (meuAtaqueMesa < defRival) {
                int rebote = defRival - meuAtaqueMesa;
                meuLP -= rebote;
                JOptionPane.showMessageDialog(janelaMesa, "A defesa dele barrou sua investida! Você sofreu rebote de " + rebote + " de LP!");
            } else {
                JOptionPane.showMessageDialog(janelaMesa, "O ATK colidiu perfeitamente com a DEF! Sem perda de pontos.");
            }

            lblMeuLp.setText(" " + jogadorLogado + " | LP: " + (meuLP < 0 ? 0 : meuLP));
            lblLpOpositor.setText("Oponente:  " + rival + " | LP: " + (opositorLP < 0 ? 0 : opositorLP));

            if (opositorLP <= 0) {
                JOptionPane.showMessageDialog(janelaMesa, "VITÓRIA! Você limpou os pontos do " + rival + "!");
                janelaMesa.dispose();
                return;
            }

            btnAtacarMesa.setEnabled(false);
            
            JOptionPane.showMessageDialog(janelaMesa, "FIM DO SEU TURNO!\n\n--- TURNO DO INIMIGO (" + rival + ") ---\n" + rival + " puxou e iniciou o contra-ataque!");
            JOptionPane.showMessageDialog(janelaMesa, " " + rival + " comanda " + monstroRival + " (ATK " + atkRival + ") para golpear seu " + minhaEscolhida + " (DEF " + minhaDefesaMesa + ")!");
            
            if (atkRival > minhaDefesaMesa) {
                int danoInimigo = atkRival - minhaDefesaMesa;
                meuLP -= danoInimigo;
                JOptionPane.showMessageDialog(janelaMesa, " Defesa violada! O impacto causou " + danoInimigo + " de dano direto nos seus Life Points!");
            } else if (atkRival < minhaDefesaMesa) {
                int reboteInimigo = minhaDefesaMesa - atkRival;
                opositorLP -= reboteInimigo;
                JOptionPane.showMessageDialog(janelaMesa, "🛡️ Excelente! Sua defesa aguentou e causou " + reboteInimigo + " de dano de rebote nele!");
            } else {
                JOptionPane.showMessageDialog(janelaMesa, "Empate absoluto no confronto! Nenhum ponto alterado.");
            }

            lblMeuLp.setText(" " + jogadorLogado + " | LP: " + (meuLP < 0 ? 0 : meuLP));
            lblLpOpositor.setText("Oponente:  " + rival + " | LP: " + (opositorLP < 0 ? 0 : opositorLP));

            if (meuLP <= 0) {
                JOptionPane.showMessageDialog(janelaMesa, "DERROTA! O oponente reduziu seus Life Points a zero.");
                janelaMesa.dispose();
            } else if (opositorLP <= 0) {
                JOptionPane.showMessageDialog(janelaMesa, " VITÓRIA COMPLETA! O inimigo caiu diante da sua parede defensiva!");
                janelaMesa.dispose();
            } else {
                JOptionPane.showMessageDialog(janelaMesa, " Campo estabilizado! Seu turno novamente, trace sua estratégia!");
                btnAtacarMesa.setEnabled(true);
            }
        });
        
        playmatTabuleiro.add(btnAtacarMesa);
        janelaMesa.add(playmatTabuleiro, BorderLayout.CENTER);
        janelaMesa.setVisible(true);
    }

    private boolean baixarImagemWeb(String urlStr, String destFisico) {
        try {
            URL url = new URL(urlStr);
            HttpURLConnection conn = (HttpURLConnection) url.openConnection();
            conn.setRequestMethod("GET"); conn.setRequestProperty("User-Agent", "Mozilla/5.0");
            if (conn.getResponseCode() == HttpURLConnection.HTTP_OK) {
                try (InputStream in = conn.getInputStream(); FileOutputStream out = new FileOutputStream(destFisico)) {
                    byte[] buffer = new byte[4096]; int length;
                    while ((length = in.read(buffer)) != -1) out.write(buffer, 0, length);
                }
                return true;
            }
            return false;
        } catch (Exception e) { return false; }
    }

    private void exibirJanelaDetalhesCarta(String nome, int atk, int def, int nivel, String nomeImagem) {
        JFrame frameDetalhes = new JFrame("Card Info - " + nome);
        frameDetalhes.setSize(500, 420);
        frameDetalhes.setLocationRelativeTo(this);
        frameDetalhes.getContentPane().setBackground(new Color(25, 28, 31)); 
        frameDetalhes.setLayout(null);

        JLabel lblFotoGrande = new JLabel("", SwingConstants.CENTER);
        lblFotoGrande.setBounds(20, 20, 220, 300);
        
        String caminhoFisico = "src/sistemayugioh/Imagem/" + nomeImagem;
        if (new File(caminhoFisico).exists()) {
            lblFotoGrande.setIcon(new ImageIcon(new ImageIcon(caminhoFisico).getImage().getScaledInstance(220, 300, Image.SCALE_SMOOTH)));
        } else {
            lblFotoGrande.setOpaque(true);
            lblFotoGrande.setBackground(new Color(40, 45, 50));
            lblFotoGrande.setText("🃏");
            lblFotoGrande.setFont(new Font("Arial", Font.BOLD, 72));
            lblFotoGrande.setForeground(new Color(50, 205, 50));
        }
        frameDetalhes.add(lblFotoGrande);

        JLabel lblTituloCarta = new JLabel(nome);
        lblTituloCarta.setFont(new Font("Arial", Font.BOLD, 22));
        lblTituloCarta.setForeground(Color.WHITE);
        lblTituloCarta.setBounds(260, 30, 220, 30);
        frameDetalhes.add(lblTituloCarta);

        JLabel lblAtkTxt = new JLabel("⚔️ ATK: " + atk);
        lblAtkTxt.setFont(new Font("Arial", Font.BOLD, 16));
        lblAtkTxt.setForeground(Color.YELLOW);
        lblAtkTxt.setBounds(260, 80, 200, 30);
        frameDetalhes.add(lblAtkTxt);

        JLabel lblDefTxt = new JLabel("🛡️ DEF (Vida): " + def);
        lblDefTxt.setFont(new Font("Arial", Font.BOLD, 16));
        lblDefTxt.setForeground(Color.CYAN);
        lblDefTxt.setBounds(260, 120, 200, 30);
        frameDetalhes.add(lblDefTxt);

        JLabel lblNivelTxt = new JLabel("⭐ Nível: " + nivel);
        lblNivelTxt.setFont(new Font("Arial", Font.BOLD, 16));
        lblNivelTxt.setForeground(Color.ORANGE);
        lblNivelTxt.setBounds(260, 160, 200, 30);
        frameDetalhes.add(lblNivelTxt);

        frameDetalhes.setVisible(true);
    
    }
    
   
    
          
    

    private void renderizarDeck() {
        painelDeckVisual.removeAll(); 

        for (int i = 0; i < cartasNome.size(); i++) {
            final int indexAtual = i;
            JPanel cardContainer = new JPanel(new BorderLayout(2, 2));
            cardContainer.setBackground(new Color(30, 25, 35)); 
            cardContainer.setPreferredSize(new Dimension(145, 205)); 
            cardContainer.setBorder(BorderFactory.createLineBorder(new Color(60, 60, 65), 1));
            cardContainer.setCursor(new Cursor(Cursor.HAND_CURSOR));

            cardContainer.addMouseListener(new MouseAdapter() {
                @Override public void mouseClicked(MouseEvent e) {
                    exibirJanelaDetalhesCarta(cartasNome.get(indexAtual), cartasAtk.get(indexAtual), cartasDef.get(indexAtual), cartasNivel.get(indexAtual), cartasImagem.get(indexAtual));
                }
            });

            JLabel lblFoto = new JLabel("", SwingConstants.CENTER);
            String caminhoFisico = "src/sistemayugioh/Imagem/" + cartasImagem.get(i); 

            if (new File(caminhoFisico).exists()) {
                lblFoto.setIcon(new ImageIcon(new ImageIcon(caminhoFisico).getImage().getScaledInstance(130, 130, Image.SCALE_SMOOTH)));
            } else {
                lblFoto.setOpaque(true); lblFoto.setBackground(new Color(40, 35, 45));
                lblFoto.setText("🃏"); lblFoto.setFont(new Font("Arial", Font.BOLD, 28));
                lblFoto.setForeground(new Color(50, 205, 50));
            }

            JLabel lblNomeCard = new JLabel(cartasNome.get(i), SwingConstants.CENTER);
            lblNomeCard.setFont(new Font("Arial", Font.BOLD, 10));
            lblNomeCard.setForeground(new Color(50, 205, 50)); 

            JLabel lblAtkCard = new JLabel("A:" + cartasAtk.get(i) + " D:" + cartasDef.get(i) + " | ⭐Nv " + cartasNivel.get(i), SwingConstants.CENTER);
            lblAtkCard.setFont(new Font("Arial", Font.BOLD, 9));
            lblAtkCard.setForeground(Color.WHITE);

            JPanel painelDadosTexto = new JPanel(new GridLayout(2, 1));
            painelDadosTexto.setBackground(new Color(30, 25, 35));
            painelDadosTexto.add(lblNomeCard); painelDadosTexto.add(lblAtkCard);

            cardContainer.add(lblFoto, BorderLayout.CENTER);
            cardContainer.add(painelDadosTexto, BorderLayout.SOUTH);

            painelDeckVisual.add(cardContainer);
        }

        painelDeckVisual.revalidate();
        painelDeckVisual.repaint();
    }

 private JButton criarBotaoElegante(String texto) {
    JButton btn = new JButton(texto);
    btn.setBackground(new Color(35, 30, 45));
    btn.setForeground(Color.WHITE);
    btn.setFont(new Font("Arial", Font.BOLD, 11));
    btn.setFocusPainted(false);
    btn.setBorder(BorderFactory.createLineBorder(new Color(70, 70, 75), 1));
    return btn;
}

private void abrirLoja() {

    String[] cartasLoja = {
        "Dragão Supremo - R$500",
        "Exodia Completo - R$800",
        "Deus Egípcio Supremo - R$1200",
        "Dragão Negro Chaos - R$400",
        "Mago Supremo das Trevas - R$600"
    };

    String escolha = (String) JOptionPane.showInputDialog(
            this,
            "Seu saldo: R$ " + treinador.getSaldo() +
            "\nEscolha uma carta:",
            " Loja",
            JOptionPane.PLAIN_MESSAGE,
            null,
            cartasLoja,
            cartasLoja[0]);

    if (escolha == null) return;

    int preco = 0;

    if (escolha.contains("Dragão Supremo")) preco = 500;
    if (escolha.contains("Exodia Completo")) preco = 800;
    if (escolha.contains("Deus Egípcio Supremo")) preco = 1200;
    if (escolha.contains("Dragão Negro Chaos")) preco = 400;
    if (escolha.contains("Mago Supremo das Trevas")) preco = 600;

  
    if (!treinador.retirarSaldo(preco)) {
        JOptionPane.showMessageDialog(
                this,
                "Saldo insuficiente!\nVocê possui apenas R$ "
                + treinador.getSaldo());
        return;
    }

   
    lblInfo.setText(
            "Duelista: " + jogadorLogado +
            " | Saldo: R$ " + treinador.getSaldo());

    if (escolha.contains("Dragão Supremo")) {
        cartasNome.add("Dragão Supremo");
        cartasAtk.add(5000);
        cartasDef.add(4500);
        cartasNivel.add(10);
        cartasImagem.add("default.jpg");
    }

    if (escolha.contains("Exodia Completo")) {
        cartasNome.add("Exodia Completo");
        cartasAtk.add(6000);
        cartasDef.add(6000);
        cartasNivel.add(12);
        cartasImagem.add("default.jpg");
    }

    if (escolha.contains("Deus Egípcio Supremo")) {
        cartasNome.add("Deus Egípcio Supremo");
        cartasAtk.add(7000);
        cartasDef.add(7000);
        cartasNivel.add(12);
        cartasImagem.add("default.jpg");
    }

    if (escolha.contains("Dragão Negro Chaos")) {
        cartasNome.add("Dragão Negro Chaos");
        cartasAtk.add(4500);
        cartasDef.add(4000);
        cartasNivel.add(9);
        cartasImagem.add("default.jpg");
    }

    if (escolha.contains("Mago Supremo das Trevas")) {
        cartasNome.add("Mago Supremo das Trevas");
        cartasAtk.add(5500);
        cartasDef.add(5000);
        cartasNivel.add(10);
        cartasImagem.add("default.jpg");
    }

    renderizarDeck();

    JOptionPane.showMessageDialog(
            this,
            "Compra realizada!\nSaldo restante: R$ "
            + treinador.getSaldo());
}
}

