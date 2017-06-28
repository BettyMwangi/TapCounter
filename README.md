# TapCounter

package com.example.hp.tapcounter;

import android.app.Activity;
import android.content.Intent;
import android.content.SharedPreferences;
import android.graphics.Color;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;

public class TapCounter extends AppCompatActivity {

    public static final String SPREFERENCE = "spref";
    TextView tv_tapped, tv_value, tv_instances;
    Button btn_tap, btnTrophy, btnReset;
    private int value = 0;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_tap_counter);

        tv_tapped = (TextView) findViewById(R.id.tv_UTapped);
        tv_value = (TextView) findViewById(R.id.tv_value);
        tv_instances = (TextView) findViewById(R.id.tv_instance);
        btn_tap = (Button) findViewById(R.id.btn_tap);
        btnTrophy = (Button) findViewById(R.id.btn_trophy);
        btnReset = (Button) findViewById(R.id.btn_reset);

       btn_tap.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                value +=1;
                tv_value.setText(""+value);
                tv_value.setTextColor(Color.BLUE);

                SharedPreferences example = getSharedPreferences(SPREFERENCE, value);
                SharedPreferences.Editor editor = example.edit();
                editor.putInt("MyValue", value);
                editor.commit();

            }
        });
        btnTrophy.setOnClickListener(new View.OnClickListener(){
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(TapCounter.this, TrophyActivity.class);
                startActivity(intent);
            }
        });
        btnReset.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                SharedPreferences pref = getSharedPreferences(SPREFERENCE, Activity.MODE_PRIVATE);
                SharedPreferences.Editor editor = pref.edit();
                editor.clear();
                editor.commit();
                value = (value - 0) - 1;
                tv_value.setText("ZERO");
            }
        });
    }
}
