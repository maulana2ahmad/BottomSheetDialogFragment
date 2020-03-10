# BottomSheetFragment-and-CountDown

### Priview
![output_5Hf9Ke](https://user-images.githubusercontent.com/43386555/76304695-638ec800-62f6-11ea-9b71-157032b22d6e.gif)  

## Class Kotlin

        class TransactionActivity : AppCompatActivity() {

            override fun onCreate(savedInstanceState: Bundle?) {
                super.onCreate(savedInstanceState)
                setContentView(R.layout.activity_transaction)

                textView_Content_PaymentDetail.setOnClickListener {
                    val view = layoutInflater.inflate(R.layout.dialog_bottom_sheet, null)
                    val dialog = BottomSheetDialog(this)
                    dialog.setContentView(view)
                    dialog.show()
                }

                button_Check_Payment_Status.setOnClickListener {
                    startActivity(Intent(this, WaitingForPaymentActivity::class.java))
                }

                //TimeCountDown()

                countDown()
            }

        //    fun TimeCountDown() {
        //
        //        val countDownTimer = object : CountDownTimer(86400000, 1000) {
        //            override fun onTick(millisUntilFinished: Long) {
        //                //Convert milliseconds into hour,minute and seconds
        //                val hms = String.format(
        //                    "%02d Hour:%02d Minute:%02d Second",
        //                    TimeUnit.MILLISECONDS.toHours(millisUntilFinished),
        //                    TimeUnit.MILLISECONDS.toMinutes(millisUntilFinished) - TimeUnit.HOURS.toMinutes(
        //                        TimeUnit.MILLISECONDS.toHours(millisUntilFinished)
        //                    ),
        //                    TimeUnit.MILLISECONDS.toSeconds(millisUntilFinished) - TimeUnit.MINUTES.toSeconds(
        //                        TimeUnit.MILLISECONDS.toMinutes(millisUntilFinished)
        //                    )
        //                )
        //                textView_TimeCountDown.setText(hms) //set text
        //            }
        //
        //            override fun onFinish() {
        //                textView_TimeCountDown.setText("TIME'S UP!!") //On finish change timer text
        //            }
        //        }.start()
        //
        //        val calendar: Calendar = Calendar.getInstance()
        //        val simpleDateFormat = SimpleDateFormat("EEEE dd MMMM yyyy HH:mm:ss a", Locale.getDefault())
        //        val strDate: String = simpleDateFormat.format(calendar.getTime())
        //
        //        runOnUiThread { textView_Day.setText("(Before " + strDate + ")") }
        //    }


            private fun countDown() {
                val countDownTimer = object : CountDownTimer(86400 * 1000, 1000) {
                    @RequiresApi(Build.VERSION_CODES.N)
                    override fun onTick(millisUntilFinished: Long) {
                        //Convert milliseconds into hour,minute and seconds
                        val hhmmss =
                            "<b>%02d</b>" + " Hours " + "<b> : </b>" + "<b>%02d</b>" + " Minute " + "<b> : </b>" + "<b>%02d</b>" + " Second"
                        val hms = String.format(
                            hhmmss,
                            TimeUnit.MILLISECONDS.toHours(millisUntilFinished),
                            TimeUnit.MILLISECONDS.toMinutes(millisUntilFinished) - TimeUnit.HOURS.toMinutes(
                                TimeUnit.MILLISECONDS.toHours(millisUntilFinished)
                            ),
                            TimeUnit.MILLISECONDS.toSeconds(millisUntilFinished) - TimeUnit.MINUTES.toSeconds(
                                TimeUnit.MILLISECONDS.toMinutes(millisUntilFinished)
                            )
                        )
                        textView_TimeCountDown.text = Html.fromHtml(hms, Html.FROM_HTML_MODE_LEGACY) //set text
                        Log.d("pesan", hms)
                    }

                    override fun onFinish() {
                        textView_TimeCountDown.setText("TIME'S UP!!") //On finish change timer text
                    }
                }
                countDownTimer.start()

                dateTimeToday()
            }

            fun dateTimeToday() {
                val today = Calendar.getInstance()
                val thatday = 86400 * 1000 + today.timeInMillis
                Log.e("thatday", thatday.toString())
                Log.e("today", today.timeInMillis.toString())
                val fmt = Calendar.getInstance()
                fmt.timeInMillis = thatday
                val formatter = SimpleDateFormat("EEEE, dd MMMM yyyy HH:mm a", Locale.getDefault())
                Log.e("pesan", formatter.format(fmt.time))
                textView_Day.text = "(Before " + formatter.format(fmt.time) + ")"
            }
        }
        
        
## Layout XML

        <?xml version="1.0" encoding="utf-8"?>
        <androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
            xmlns:app="http://schemas.android.com/apk/res-auto"
            xmlns:tools="http://schemas.android.com/tools"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            tools:context=".TransactionActivity">

            <com.google.android.material.appbar.AppBarLayout
                android:id="@+id/app_bar"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:backgroundTint="@android:color/white"
                app:layout_constraintStart_toStartOf="parent"
                app:layout_constraintTop_toTopOf="parent">

                <androidx.appcompat.widget.Toolbar
                    android:id="@+id/toolbar"
                    android:layout_width="match_parent"
                    android:layout_height="wrap_content"
                    app:navigationIcon="@drawable/ic_arrow_back">

                    <TextView
                        android:id="@+id/toolbar_title"
                        android:layout_width="wrap_content"
                        android:layout_height="wrap_content"
                        android:layout_gravity="center"
                        android:text="Transaction"
                        android:textColor="@android:color/black"
                        android:textSize="16sp" />

                </androidx.appcompat.widget.Toolbar>

            </com.google.android.material.appbar.AppBarLayout>

            <androidx.constraintlayout.widget.ConstraintLayout
                android:id="@+id/constrainlayout"
                android:layout_width="0dp"
                android:layout_height="wrap_content"
                android:layout_marginStart="20dp"
                android:layout_marginLeft="20dp"
                android:layout_marginTop="18dp"
                android:layout_marginEnd="20dp"
                android:layout_marginRight="20dp"
                android:background="@drawable/bg_color_orange"
                app:layout_constraintEnd_toEndOf="parent"
                app:layout_constraintHorizontal_bias="0.0"
                app:layout_constraintStart_toStartOf="parent"
                app:layout_constraintTop_toBottomOf="@+id/app_bar">

                <TextView
                    android:id="@+id/textView_Title"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:layout_marginTop="18dp"
                    android:text="Please make a payment Immediatelly"
                    android:textColor="@android:color/black"
                    app:layout_constraintEnd_toEndOf="@+id/textView_TimeCountDown"
                    app:layout_constraintStart_toStartOf="@+id/textView_TimeCountDown"
                    app:layout_constraintTop_toTopOf="@+id/constrainlayout" />

                <TextView
                    android:id="@+id/textView_TimeCountDown"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:layout_marginStart="32dp"
                    android:layout_marginLeft="32dp"
                    android:layout_marginTop="16dp"
                    android:layout_marginEnd="32dp"
                    android:layout_marginRight="32dp"
                    android:text="13 Hour: 59 Minute: 21 Second"
                    android:textColor="@android:color/black"
                    android:textSize="20sp"
                    app:layout_constraintEnd_toEndOf="parent"
                    app:layout_constraintStart_toStartOf="parent"
                    app:layout_constraintTop_toBottomOf="@+id/textView_Title" />

        <!--        <TextView-->
        <!--            android:id="@+id/tv_hours"-->
        <!--            android:layout_width="wrap_content"-->
        <!--            android:layout_height="wrap_content"-->
        <!--            android:layout_marginTop="18dp"-->
        <!--            android:text="13"-->
        <!--            android:textColor="@android:color/black"-->
        <!--            android:textSize="22sp"-->
        <!--            app:layout_constraintStart_toStartOf="@+id/textView_Title"-->
        <!--            app:layout_constraintTop_toBottomOf="@+id/textView_Title" />-->

        <!--        <TextView-->
        <!--            android:id="@+id/tv_hpurs_title"-->
        <!--            android:layout_width="wrap_content"-->
        <!--            android:layout_height="wrap_content"-->
        <!--            android:text="Hour:"-->
        <!--            android:textColor="@android:color/black"-->
        <!--            android:textSize="22sp"-->
        <!--            app:layout_constraintBottom_toBottomOf="@+id/tv_hours"-->
        <!--            app:layout_constraintEnd_toEndOf="@+id/textView_Title"-->
        <!--            app:layout_constraintHorizontal_bias="0.025"-->
        <!--            app:layout_constraintStart_toEndOf="@+id/tv_hours"-->
        <!--            app:layout_constraintTop_toTopOf="@+id/tv_hours"-->
        <!--            app:layout_constraintVertical_bias="0.0" />-->

        <!--        <TextView-->
        <!--            android:id="@+id/tv_min"-->
        <!--            android:layout_width="wrap_content"-->
        <!--            android:layout_height="wrap_content"-->
        <!--            android:text="59"-->
        <!--            android:textColor="@android:color/black"-->
        <!--            android:textSize="22sp"-->
        <!--            app:layout_constraintBottom_toBottomOf="@+id/tv_hpurs_title"-->
        <!--            app:layout_constraintEnd_toEndOf="@+id/textView_Title"-->
        <!--            app:layout_constraintHorizontal_bias="0.0"-->
        <!--            app:layout_constraintStart_toEndOf="@+id/tv_hpurs_title"-->
        <!--            app:layout_constraintTop_toTopOf="@+id/tv_hpurs_title"-->
        <!--            app:layout_constraintVertical_bias="0.0" />-->

        <!--        <TextView-->
        <!--            android:id="@+id/tv_min_title"-->
        <!--            android:layout_width="wrap_content"-->
        <!--            android:layout_height="wrap_content"-->
        <!--            android:layout_marginTop="16dp"-->
        <!--            android:text="Minute:"-->
        <!--            android:textColor="@android:color/black"-->
        <!--            android:textSize="22sp"-->
        <!--            app:layout_constraintBottom_toBottomOf="@+id/tv_min"-->
        <!--            app:layout_constraintHorizontal_bias="0.0"-->
        <!--            app:layout_constraintStart_toEndOf="@+id/tv_min"-->
        <!--            app:layout_constraintTop_toTopOf="@+id/tv_min"-->
        <!--            app:layout_constraintVertical_bias="1.0" />-->

        <!--        <TextView-->
        <!--            android:id="@+id/tv_sec"-->
        <!--            android:layout_width="wrap_content"-->
        <!--            android:layout_height="wrap_content"-->
        <!--            android:text="21"-->
        <!--            android:textColor="@android:color/black"-->
        <!--            android:textSize="22sp"-->
        <!--            app:layout_constraintBottom_toBottomOf="@+id/tv_min_title"-->
        <!--            app:layout_constraintHorizontal_bias="0.0"-->
        <!--            app:layout_constraintStart_toEndOf="@+id/tv_min_title"-->
        <!--            app:layout_constraintTop_toTopOf="@+id/tv_min_title"-->
        <!--            app:layout_constraintVertical_bias="0.0" />-->

        <!--        <TextView-->
        <!--            android:id="@+id/tv_sec_title"-->
        <!--            android:layout_width="wrap_content"-->
        <!--            android:layout_height="wrap_content"-->
        <!--            android:text="Secon"-->
        <!--            android:textColor="@android:color/black"-->
        <!--            android:textSize="22sp"-->
        <!--            app:layout_constraintBottom_toBottomOf="@+id/tv_sec"-->
        <!--            app:layout_constraintEnd_toEndOf="@+id/textView_Title"-->
        <!--            app:layout_constraintHorizontal_bias="0.0"-->
        <!--            app:layout_constraintStart_toEndOf="@+id/tv_sec"-->
        <!--            app:layout_constraintTop_toTopOf="@+id/tv_sec"-->
        <!--            app:layout_constraintVertical_bias="0.0" />-->

                <TextView
                    android:id="@+id/textView_Day"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:layout_marginTop="16dp"
                    android:layout_marginBottom="18dp"
                    android:text="(Before Thursday, 16 January 2020, 13:33 WIB)"
                    android:textColor="@android:color/black"
                    app:layout_constraintBottom_toBottomOf="parent"
                    app:layout_constraintEnd_toEndOf="@+id/textView_TimeCountDown"
                    app:layout_constraintStart_toStartOf="@+id/textView_TimeCountDown"
                    app:layout_constraintTop_toBottomOf="@id/textView_TimeCountDown" />

            </androidx.constraintlayout.widget.ConstraintLayout>

            <TextView
                android:id="@+id/textView"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_marginTop="18dp"
                android:text="Payment Transfer To Virtual Account"
                android:textColor="@android:color/black"
                app:layout_constraintStart_toStartOf="@+id/constrainlayout"
                app:layout_constraintTop_toBottomOf="@+id/constrainlayout" />

            <ImageView
                android:id="@+id/imageView_icon_bank_mandiri"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_marginTop="18dp"
                android:src="@drawable/ic_bank_mandiri"
                app:layout_constraintStart_toStartOf="@+id/textView"
                app:layout_constraintTop_toBottomOf="@+id/textView" />


            <TextView
                android:id="@+id/textView_No_VirtualAccount"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_marginStart="16dp"
                android:layout_marginLeft="16dp"
                android:text="123 45678912"
                android:textColor="@android:color/black"
                android:textSize="20sp"
                android:textStyle="bold"
                app:layout_constraintBottom_toBottomOf="@+id/imageView_icon_bank_mandiri"
                app:layout_constraintStart_toEndOf="@+id/imageView_icon_bank_mandiri"
                app:layout_constraintTop_toTopOf="@+id/imageView_icon_bank_mandiri" />

            <ImageView
                android:id="@+id/imageView_icon_copy"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_marginStart="18dp"
                android:layout_marginLeft="18dp"
                android:src="@drawable/ic_copy"
                app:layout_constraintBottom_toBottomOf="@+id/textView_No_VirtualAccount"
                app:layout_constraintStart_toEndOf="@+id/textView_No_VirtualAccount"
                app:layout_constraintTop_toTopOf="@+id/textView_No_VirtualAccount" />

            <View
                android:id="@+id/view_view"
                android:layout_width="0dp"
                android:layout_height="2dp"
                android:layout_marginTop="18dp"
                android:background="#CDCDCD"
                app:layout_constraintEnd_toEndOf="@+id/constrainlayout"
                app:layout_constraintStart_toStartOf="@+id/constrainlayout"
                app:layout_constraintTop_toBottomOf="@+id/textView_No_VirtualAccount" />

            <TextView
                android:id="@+id/textView_Amount"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_marginTop="18dp"
                android:text="Amount To Be Paid"
                android:textColor="@android:color/black"
                app:layout_constraintStart_toStartOf="@+id/view_view"
                app:layout_constraintTop_toBottomOf="@+id/view_view" />

            <TextView
                android:id="@+id/textView_AmountRp"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_marginTop="8dp"
                android:text="Rp. 150.210"
                android:textColor="@android:color/black"
                android:textSize="20sp"
                android:textStyle="bold"
                app:layout_constraintStart_toStartOf="@+id/textView_Amount"
                app:layout_constraintTop_toBottomOf="@+id/textView_Amount" />

            <ImageView
                android:id="@+id/imageView_icon_copy2"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_marginStart="18dp"
                android:layout_marginLeft="18dp"
                android:src="@drawable/ic_copy"
                app:layout_constraintBottom_toBottomOf="@+id/textView_AmountRp"
                app:layout_constraintStart_toEndOf="@+id/textView_AmountRp"
                app:layout_constraintTop_toTopOf="@+id/textView_AmountRp" />

            <TextView
                android:id="@+id/textView_Content_PaymentDetail"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_marginTop="18dp"
                android:paddingTop="6dp"
                android:paddingBottom="10dp"
                android:text="Payment Details"
                android:textColor="#FF8830"
                app:layout_constraintStart_toStartOf="@+id/textView_AmountRp"
                app:layout_constraintTop_toBottomOf="@+id/textView_AmountRp" />

            <Button
                android:id="@+id/button_Check_Payment_Status"
                android:layout_width="0dp"
                android:layout_height="wrap_content"
                android:layout_marginTop="20dp"
                android:background="@drawable/bg_color_orange2"
                android:text="Check Payment Status"
                android:textColor="@android:color/white"
                app:layout_constraintBottom_toTopOf="@+id/button2"
                app:layout_constraintEnd_toEndOf="@+id/constrainlayout"
                app:layout_constraintStart_toStartOf="@+id/constrainlayout"
                app:layout_constraintTop_toBottomOf="@+id/textView_Content_PaymentDetail" />

            <Button
                android:id="@+id/button2"
                android:layout_width="0dp"
                android:layout_height="wrap_content"
                android:layout_marginTop="15dp"
                android:background="@drawable/bg_color_orange_stroke"
                android:text="Back To Home"
                android:textColor="#FF8830"
                app:layout_constraintEnd_toEndOf="@+id/button_Check_Payment_Status"
                app:layout_constraintStart_toStartOf="@+id/button_Check_Payment_Status"
                app:layout_constraintTop_toBottomOf="@+id/button_Check_Payment_Status" />

        </androidx.constraintlayout.widget.ConstraintLayout>
