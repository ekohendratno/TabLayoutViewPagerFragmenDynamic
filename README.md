# TabLayoutViewPagerFragmenDynamic

TabLayout with ViewPager Fragmen Dynamic

# Screenshoot

![Screenshot](https://github.com/ekohendratno/TabLayoutViewPagerFragmenDynamic/blob/master/sc1.png)
![Screenshot](https://github.com/ekohendratno/TabLayoutViewPagerFragmenDynamic/blob/master/sc2.png)

# Step
## lyt_aktivityku.xml

<?xml version="1.0" encoding="utf-8"?>
<android.support.design.widget.CoordinatorLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:fitsSystemWindows="true"
    tools:context="id.kopas.berkarya.jadwalsekolah.Activityku">

    <android.support.design.widget.AppBarLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:theme="@style/AppTheme.AppBarOverlay">

        <android.support.v7.widget.Toolbar
            android:id="@+id/toolbar"
            android:layout_width="match_parent"
            android:layout_height="?attr/actionBarSize"
            android:background="?attr/colorPrimary"
            app:layout_scrollFlags="scroll|enterAlways"
            app:popupTheme="@style/AppTheme.PopupOverlay">

        <TextView
            android:id="@+id/toolbar_title"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            style="@style/TextAppearance.AppCompat.Widget.ActionBar.Title"
            android:layout_gravity="center" />

        </android.support.v7.widget.Toolbar>

        <android.support.design.widget.TabLayout
            android:id="@+id/tabs"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:background="@android:color/transparent"
            app:tabGravity="fill"
            app:tabMode="scrollable"
            app:tabTextAppearance="@style/TextAppearance.Design.Tab"
            android:overScrollMode="never" />

    </android.support.design.widget.AppBarLayout>


    <android.support.v4.view.ViewPager
        android:id="@+id/viewPager"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        app:layout_behavior="@string/appbar_scrolling_view_behavior" />


    <android.support.design.widget.FloatingActionButton
        android:id="@+id/fab"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="bottom|end"
        android:layout_margin="@dimen/fab_margin"
        app:srcCompat="@drawable/ic_add_white_24dp" />

</android.support.design.widget.CoordinatorLayout>


## fragment.xml

<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingLeft="16dp"
    android:paddingRight="16dp"
    tools:context="id.kopas.berkarya.jadwalsekolah.Activityku">

    <android.support.v7.widget.RecyclerView
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:id="@+id/recyclerView"/>
    <TextView
        android:id="@+id/empty_view"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:gravity="center"
        android:visibility="gone"
        android:text="@string/no_data_available" />

</RelativeLayout>


## Activityku.java

.....

public class Activityku extends AppCompatActivity {

    private DatabaseHelper db;
    TabLayout tabLayout;
    ViewPager viewPager;
    ViewPagerAdapter viewPagerAdapter;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        ....


        tabLayout = (TabLayout) findViewById(R.id.tabs);
        viewPager = (ViewPager) findViewById(R.id.viewPager);

        .......

        ArrayList<String> tabtitles = new ArrayList<>();
        tabtitles.add("Minggu");
        tabtitles.add("Senin");
        tabtitles.add("Selasa");
        tabtitles.add("Rabu");
        tabtitles.add("Kamis");
        tabtitles.add("Jumat");
        tabtitles.add("Sabtu");

        viewPagerAdapter = new ViewPagerAdapter(getSupportFragmentManager(),tabtitles);
        viewPager.setAdapter(viewPagerAdapter);


        tabLayout.setupWithViewPager(viewPager);
    }

    public static class ViewPagerAdapter extends FragmentPagerAdapter {
        ArrayList<String> tabtitles = new ArrayList<>();

        public ViewPagerAdapter(FragmentManager fragmentManager, ArrayList<String> tabtitles) {
            super(fragmentManager);
            this.tabtitles = tabtitles;
        }

        @Override
        public Fragment getItem(int position) {
            return PlaceholderFragment .newInstance(tabtitles.get(position));
        }

        @Override
        public int getCount() {
            return tabtitles.size();
        }

        @Override
        public CharSequence getPageTitle(int position) {
            return tabtitles.get(position);
        }
    }

    public static class PlaceholderFragment extends Fragment {

        ....

        /**
         * Returns a new instance of this fragment for the given section
         * number.
         */
        public static PlaceholderFragment newInstance(String text) {
            PlaceholderFragment fragment = new PlaceholderFragment();
            Bundle args = new Bundle();
            args.putString(ARG_SECTION_NUMBER, text);
            fragment.setArguments(args);
            return fragment;
        }

        .....
    }

    ....
}
