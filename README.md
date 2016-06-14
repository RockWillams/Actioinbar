# Actioinbar
ActionBar actionBar = getActionBar();
 actionBar.setNavigationMode(ActionBar.NAVIGATION_MODE_TABS);
ViewPager viewPager = (ViewPager) findViewById(R.id.pager);
SelectionsPagerAdapter adapter = new SectionsPagerAdapter(getSupportFragmentViewPager());
viewPager.setViewPagerAdapter(new SectionsPagerAdapter(getSupportFragmentViewPager()));
viewPager.setOnPageListner(new ViewPageListner(){
      @OverWrite
      onPageListner(int position){
          actionBar.setSelectedNavigationItem(position);
      }
      


});
for(int i= 0;i<adapter.getCount();i++){
    ActionBar.Tab tab = new ActionBar.Tab();
    tab.setText(adapter.getTitle(i));
    tab.setTabListner(this);
    actionBar.add(tab);
}










public class SectionsPagerAdapter extends FragmentPagerAdapter {

    // Stores the instances of the pages
    private ArrayList<Fragment> fragments = null;

    /**
     * Only Constructor, requires a the activity's fragment managers
     * 
     * @param fragmentManager
     */
    public SectionsPagerAdapter(FragmentManager fragmentManager) {
      super(fragmentManager);
      fragments = new ArrayList<Fragment>();
      // create the history view, passes the client handle as an argument
      // through a bundle
      Fragment fragment = new HistoryFragment();
      Bundle args = new Bundle();
      args.putString("handle", getIntent().getStringExtra("handle"));
      fragment.setArguments(args);
      // add all the fragments for the display to the fragments list
      fragments.add(fragment);
      fragments.add(new SubscribeFragment());
      fragments.add(new PublishFragment());

    }

    /**
     * @see android.support.v4.app.FragmentPagerAdapter#getItem(int)
     */
    @Override
    public Fragment getItem(int position) {
      return fragments.get(position);
    }

    /**
     * @see android.support.v4.view.PagerAdapter#getCount()
     */
    @Override
    public int getCount() {
      return fragments.size();
    }

    /**
     * 
     * @see FragmentPagerAdapter#getPageTitle(int)
     */
    @Override
    public CharSequence getPageTitle(int position) {
      switch (position) {
        case 0 :
          return getString(R.string.history).toUpperCase();
        case 1 :
          return getString(R.string.subscribe).toUpperCase();
        case 2 :
          return getString(R.string.publish).toUpperCase();
      }
      // return null if there is no title matching the position
      return null;
    }

  }
