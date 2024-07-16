import com.google.gson.Gson;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;
import java.util.Scanner;

public class CurrencyConverter {

    private static final String API_KEY = "your_api_key"; // Substitua pela sua chave da API
    private static final String API_URL = "https://api.exchangerate-api.com/v4/latest/";

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Menu de opções
        System.out.println("Escolha uma opção de conversão:");
        System.out.println("1. Dólar para Real");
        System.out.println("2. Real para Dólar");
        System.out.println("3. Euro para Real");
        System.out.println("4. Real para Euro");
        System.out.println("5. Libra para Real");
        System.out.println("6. Real para Libra");
        
        int opcao = scanner.nextInt();

        System.out.print("Digite o valor que deseja converter: ");
        double valor = scanner.nextDouble();

        double taxa = obterTaxaConversao(opcao);
        double valorConvertido = valor * taxa;

        System.out.printf("O valor convertido é: %.2f%n", valorConvertido);
    }

    private static double obterTaxaConversao(int opcao) {
        String baseCurrency = "";
        String targetCurrency = "";

        switch (opcao) {
            case 1:
                baseCurrency = "USD";
                targetCurrency = "BRL";
                break;
            case 2:
                baseCurrency = "BRL";
                targetCurrency = "USD";
                break;
            case 3:
                baseCurrency = "EUR";
                targetCurrency = "BRL";
                break;
            case 4:
                baseCurrency = "BRL";
                targetCurrency = "EUR";
                break;
            case 5:
                baseCurrency = "GBP";
                targetCurrency = "BRL";
                break;
            case 6:
                baseCurrency = "BRL";
                targetCurrency = "GBP";
                break;
            default:
                System.out.println("Opção inválida!");
                System.exit(0);
        }

        String jsonString = getJsonResponse(baseCurrency);
        Gson gson = new Gson();
        ApiResponse response = gson.fromJson(jsonString, ApiResponse.class);
        
        return response.rates.get(targetCurrency);
    }

    private static String getJsonResponse(String baseCurrency) {
        StringBuilder result = new StringBuilder();
        try {
            URL url = new URL(API_URL + baseCurrency + "?apikey=" + API_KEY);
            HttpURLConnection conn = (HttpURLConnection) url.openConnection();
            conn.setRequestMethod("GET");
            InputStreamReader reader = new InputStreamReader(conn.getInputStream());
            int read;
            while ((read = reader.read()) != -1) {
                result.append((char) read);
            }
            reader.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
        return result.toString();
    }

    class ApiResponse {
        public String base;
        public java.util.Map<String, Double> rates;
    }
}

