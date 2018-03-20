# AndroidParkEase

//Starts here******************
package com.example.a300273028.parkease;

import android.support.design.widget.TabLayout;
import android.support.v4.app.FragmentTransaction;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.widget.TextView;

public class MainActivity extends AppCompatActivity {
    private boolean isFragmentDisplayed = false;

    static final String STATE_FRAGMENT = "state_of_fragment";


    TabLayout tabLayout;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        tabLayout = (TabLayout)findViewById(R.id.tabLayout);
      //  final TextView test=(TextView)findViewById(R.id.testText);

        tabLayout.addOnTabSelectedListener(new TabLayout.OnTabSelectedListener() {
            @Override
            public void onTabSelected(TabLayout.Tab tab) {
                if(tab.getPosition() == 1 )
                {
                   // test.setText("wowwww");
                    displayFragment();
                }
                else if(tab.getPosition() == 0)
                {

                  //  test.setText("Not so wooww");
                    closeFragment();

                }
            }

            @Override
            public void onTabUnselected(TabLayout.Tab tab) {

            }

            @Override
            public void onTabReselected(TabLayout.Tab tab) {

            }
        });



    }
    public void onSaveInstanceState(Bundle saveInstanceStates) {
        saveInstanceStates.putBoolean(STATE_FRAGMENT, isFragmentDisplayed);
        super.onSaveInstanceState(saveInstanceStates);
    }


    public void displayFragment()
    {
        UserFragment simpleFragment = UserFragment.newInstance();

        android.support.v4.app.FragmentManager fragmentManager = getSupportFragmentManager();
        FragmentTransaction fragmentTransaction = fragmentManager.beginTransaction();

        fragmentTransaction.add(R.id.fragment_container, simpleFragment).addToBackStack(null).commit();
     //   isFragmentDisplayed = true;

    }
    public void closeFragment()

    {
        android.support.v4.app.FragmentManager fragmentManager = getSupportFragmentManager();
        UserFragment userFragment=(UserFragment) fragmentManager.findFragmentById(R.id.fragment_container);
        FragmentTransaction fragmentTransaction = fragmentManager.beginTransaction();
        fragmentTransaction.remove(userFragment).commit();
    }


}
