import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

import org.json.simple.JSONArray;
import org.json.simple.JSONObject;
import org.json.simple.parser.JSONParser;

public class DataExtract {
    public static void main(String[] args) {
        try {
            URL url = new URL("https://api.thingspeak.com/channels/875453/feeds.json?api_key=1DSQ7R1XTT1OK0Z1&results=20");
            HttpURLConnection con =(HttpURLConnection) url.openConnection();
            con.setRequestMethod("GET");

            InputStreamReader read =new InputStreamReader(con.getInputStream());
            BufferedReader bread = new BufferedReader(read);

            String str= bread.readLine();
            System.out.println(str);
            bread.close();

            JSONParser jpar = new JSONParser();
            JSONObject jobj= (JSONObject) jpar.parse(str);
            JSONObject jobj1= (JSONObject)jobj.get("channel");
            
            System.out.println("id:"+jobj1.get("id"));
            System.out.println("name:"+jobj1.get("name"));

            JSONArray jarr = (JSONArray)jobj.get("feeds");
            for(int i=0;i<jarr.size();i++){
                JSONObject jobj2 = (JSONObject)jarr.get(i);
                System.out.println("field1:"+jobj2.get("field1"));
            }



            
        } catch (Exception e) {
            
        }
    }
    
}
