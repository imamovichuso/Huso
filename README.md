
package com.imamovchuso.appeuro;

import java.util.Map;

import org.apache.http.Header;
import org.json.JSONException;
import org.json.JSONObject;

import android.os.Bundle;
import android.support.v7.app.ActionBarActivity;
import android.util.Log;
import android.view.View;
import android.view.View.OnClickListener;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;
import android.widget.Toast;

import com.loopj.android.http.AsyncHttpClient;
import com.loopj.android.http.AsyncHttpResponseHandler;

//@SuppressWarnings("deprecation")
@SuppressWarnings("deprecation")
public class MainActivity extends ActionBarActivity {

	private static final String API_URL = "http://api.fixer.io/latest";


	//@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.activity_main);
		Button btnSTART =(Button)findViewById(R.id.button1);
		final EditText eurValue = (EditText) findViewById(R.id.euro);
		final TextView chfValue = (TextView) findViewById(R.id.gbp);
		final TextView usdValue = (TextView) findViewById(R.id.usd);
			btnSTART.setOnClickListener(new OnClickListener() {
			public void onClick(View arg0){
				
				if (!eurValue.getText().toString().equals("")) {
					AsyncHttpClient client = new AsyncHttpClient();
					client.get(API_URL, new AsyncHttpResponseHandler() {

						//  @Override
						//public void onSuccess(String response) {
						//Log.i("APPEURO","HTTP Sucess" );

						@Override
						public void onFailure(int arg0, Header[] arg1,
								byte[] arg2, Throwable arg3) {
							// TODO Auto-generated method stub
							
						}

						@Override
						public void onSuccess(int arg0, Header[] arg1,
								byte[] arg2) {
							// TODO Auto-generated method stub
							Log.i("APPEURO", "HTTP Sucess");
						
							try {

								Map response = null;
								//String response = null;
								JSONObject jsonObj = new JSONObject(response);
								JSONObject ratesObject = jsonObj
										.getJSONObject("rates");
								Double gbpRate = ratesObject.getDouble("GBP");
								Double usdRate = ratesObject.getDouble("USD");
								//Log.i("APPEURO", response);
								Log.i("APPEURO", "GBP:" + gbpRate);
								Log.i("APPEURO", "USD:" + usdRate);
								
								//Double Euro =Double.valueOf(eurValue.getText().toString());
								
									Double Euro = Double.valueOf(eurValue
											.getText().toString());
									Double CHFS = Euro * gbpRate;
									Double usds = Euro * usdRate;
									chfValue.setText("GBP:"
											+ String.valueOf(CHFS));
									usdValue.setText("USD:"
											+ String.valueOf(usds));
								 
							}

							catch (JSONException a) {
								a.printStackTrace();
							}

						}

						
					});
				}else {
						Toast.makeText(getApplicationContext(),
								"Bitte ENTER in EUR value",
								Toast.LENGTH_LONG).show();

					}
				}
			
				
			
			
		});
	}}
				
				
			
			
			
			
			
			

