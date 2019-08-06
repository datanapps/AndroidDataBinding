# AndroidDataBinding
Now very easy to bind data and it's view (data binding) in android

![alt text](https://github.com/datanapps/NightMode/blob/master/screens/screens.jpg)


### Download APK : 

https://github.com/datanapps/AndroidDataBinding/blob/master/screens/app-debug.apk

Its have just a few steps :

#### Benifits:

1. Data binding can lead to faster development times
2. Faster execution times (more then findviewbyid)
3. Stronger readability (More readable and maintained code).
4. Remove boilerplate code

#### Drawback :

1. Auto generated class (it's true it will increase the app size)
2. Hard to debug - depends, like readability, of what you are used to.


#### Add the dataBinding element to your app build.gradle file to enable Data Binding.
      android {
      dataBinding.enabled = true
      }

activity_book_detail.xml

                  <?xml version="1.0" encoding="utf-8"?>
                  <layout xmlns:android="http://schemas.android.com/apk/res/android"
                     >

                      <data>
                          <variable name="book" type="com.example.androiddatabinding.Book"/>
                      </data>

                      <androidx.constraintlayout.widget.ConstraintLayout
                          xmlns:app="http://schemas.android.com/apk/res-auto"
                          xmlns:tools="http://schemas.android.com/tools"
                          android:layout_width="match_parent"
                          android:layout_height="match_parent"
                          tools:context=".BookDetailActivity"
                         >

                      <TextView
                          android:id="@+id/name"
                          android:layout_width="wrap_content"
                          android:layout_height="wrap_content"
                          android:text="@{book.name}"
                          android:textSize="20sp"
                          android:textStyle="bold"
                          app:layout_constraintBottom_toBottomOf="parent"
                          app:layout_constraintLeft_toLeftOf="parent"
                          app:layout_constraintRight_toRightOf="parent"
                          app:layout_constraintTop_toTopOf="parent" />


                      <TextView
                          android:id="@+id/email"
                          android:layout_width="wrap_content"
                          android:layout_height="wrap_content"
                          android:text="@{book.email}"
                          android:textSize="20sp"
                          app:layout_constraintLeft_toLeftOf="parent"
                          app:layout_constraintRight_toRightOf="parent"
                          app:layout_constraintTop_toBottomOf="@+id/name" />
                      </androidx.constraintlayout.widget.ConstraintLayout>
                  </layout>
                  
 Model : Book.class
                  
       package com.example.androiddatabinding;

            public class Book {

                private String name;
                private String email;

                public Book(String name, String email) {
                    this.name = name;
                    this.email = email;
                }
                public String getName() {
                    return name;
                }

                public void setName(String name) {
                    this.name = name;
                }

                public String getEmail() {
                    return email;
                }

                public void setEmail(String email) {
                    this.email = email;
                }
            }

Activity : BookDetailActivity.class


      public class BookDetailActivity extends AppCompatActivity {
          @Override
          protected void onCreate(Bundle savedInstanceState) {
              super.onCreate(savedInstanceState);
              //setContentView(R.layout.activity_book_detail);

              ActivityBookDetailBinding binding = DataBindingUtil.setContentView(this, R.layout.activity_book_detail);
              Book book = new Book("Book", "book@gmail.com");
              binding.setBook(book);
          }
      }
