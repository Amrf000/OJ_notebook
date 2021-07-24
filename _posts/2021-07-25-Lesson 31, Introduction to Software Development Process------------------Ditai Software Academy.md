---
layout: post
title: Lesson 31, Introduction to Software Development Process
category: qt5
tags: [qt5]
---
# 

# 1\. Software development process

1\. What is the software development process

(1), through a series of steps to ensure the smooth completion of the software product

(2) Management methodology of software products during the life cycle

2\. The essence of the software development process

(1) The development process has nothing to do with specific technology

(2) The development process is a rule that the development team must follow

3\. Common software development process

(1), improvisation model (Build-and-Fix Model)

A. Start development immediately after communicating with end users

B. There is no need analysis and demand discovery process

C. There is no overall design and planning process

D. There is no relevant software documentation and poor maintainability

(2) Waterfall Model

A. The core idea of ​​the waterfall model is to simplify the problem according to the process, separate the realization of the function from the design, and facilitate the division of labor and cooperation, that is, the use of structured analysis and design methods to separate the logical realization from the physical realization.

B. Divide the software life cycle into six basic activities: planning, demand analysis → software design → program writing → software testing → release, operation and maintenance, and stipulate their top-down, fixed sequence of interconnection, like a waterfall Flowing water, falling step by step.

C. Provide checkpoints divided by stages for the project. After the current stage is completed, just focus on the subsequent stages.

D. Since the development steps are linear and irreversible, users can only see the development results until the end of the entire process, which increases development risks.

(3), incremental model (Incremental Model)

A. The system function is decomposed into non-overlapping sub-functions. It introduces the concept of incremental packages. You don't need to wait until all the requirements are released. Development can be carried out as long as the incremental package of a certain requirement is released. Although a certain incremental package may need to be further adapted to the needs of the customer and changed, as long as the incremental package is small enough, its impact can be bearable for the entire project.

B. Fully implement one sub-function each time. Since only part of the user's functions are submitted each time, users have more time to learn and adapt to new products.

C. The incremental model combines the basic components (repetitive application) of the waterfall model and the iterative features of the prototype implementation. The model uses linear sequences that are staggered as the schedule progresses, and each linear sequence produces a releaseable "increment" of the software. When using the incremental model, the first incremental is often the core product, that is, the first incremental achieves the basic requirements, but many supplementary features have not been released. The customer's use and evaluation of each incremental release is regarded as the new feature and function of the next incremental release. This process is repeated after each incremental release until the final perfect product is produced.

D. After all the sub-functions are completed, the system development ends.

![](/md_blog/public/assets/2021-07-25/efae4ea0ad492c4321c3031e8e8d7cbb.JPEG)

(4) Spiral Model

A. Adopt an iterative method for system development, which combines the waterfall model and the rapid prototyping model.

B. The software project is broken down into multiple different versions to complete

C. The development process of each version requires user participation

D. Plan the next version based on the feedback of the previous version

E. The risk-driven spiral model is suitable for large-scale software projects developed internally, but only when the developers have experience and expertise in risk analysis and risk elimination can the use of this model be successful.

![](/md_blog/public/assets/2021-07-25/88a1854cceeece43dcad7aded70e2749.png)

(5) Agile Modeling

![](/md_blog/public/assets/2021-07-25/76dd160e3a5dd41eaa39b9ac74c7a0d7.JPEG) 

A. Keep everything simple

B. Embrace change

C. Work efficiently

D. Continuous development

4\. Incremental model is suitable for the development of text editors

(1) Relatively fixed demand

(2) Weak coupling between functions

![](/md_blog/public/assets/2021-07-25/9e6490d00db35fbe5859e222e5686548.JPEG) 

NotePad.pro project phase test (for memory leak detection: valgrind tool)

![](/md_blog/public/assets/2021-07-25/d2b88b779cfe3245b75c40ea465a4ccd.gif) MainWindow.h
    

1. #ifndef MAINWINDOW_H
    

2. #define MAINWINDOW_H
    

3. #include <QMenuBar>
    

4. #include <QMenu>
    

5. #include <QAction>
    

6. #include <QString>
    

7. #include <QtGui/QMainWindow>
    

8. #include <QToolBar>
    

9. #include <QIcon>
    

10. #include <QSize>
    

11. #include <QStatusBar>
    

12. #include <QLabel>
    

13. #include <QPlainTextEdit>
    

14. class MainWindow : public QMainWindow
    

15. {
    

16.  Q_OBJECT
    

17. private:
    

18.  QPlainTextEdit mainEdit;
    

19.  QLabel statusLabel;
    

20.  MainWindow(QWidget *parent = 0);
    

21.  MainWindow(const MainWindow& obj);
    

22.  MainWindow* operator = (const MainWindow& obj);
    

23.  bool construct();
    

24. 25.  bool initMenuBar();//Menu bar
    

26.  bool initToolBar();//Toolbar
    

27.  bool initStatusBar();//Status bar
    

28.  bool initinitMainEditor();//Edit window
    

29. 30.  bool initFileMenu(QMenuBar* mb);//File menu
    

31.  bool initEditMenu(QMenuBar* mb);//Edit menu
    

32.  bool initFormatMenu(QMenuBar* mb);//Format menu
    

33.  bool initViewMenu(QMenuBar* mb);//View menu
    

34.  bool initHelpMenu(QMenuBar* mb);//Help menu
    

35. 36.  bool initFileToolItem(QToolBar* tb);//Tool options
    

37.  bool initEditToolItem(QToolBar* tb);
    

38.  bool initFormatToolItem(QToolBar* tb);
    

39.  bool initViewToolItem(QToolBar* tb);
    

40. 41. 42.  bool makeAction(QAction*& action,QMenu* menu, QString text, int key);//menu item
    

43.  bool makeAction(QAction*& action,QToolBar* tb, QString tip, QString icon);
    

44. public:
    

45.  static MainWindow* NewInstance();
    

46.  ~MainWindow();
    

47. };
    

48. 49. #endif // MAINWINDOW_H
    

50. 51. MainWindow.h
    
    

![](/md_blog/public/assets/2021-07-25/d2b88b779cfe3245b75c40ea465a4ccd.gif) MainWindow.cpp
    

1. #include "MainWindow.h"
    

2. #include <QDebug>
    

3. 4. MainWindow::MainWindow(QWidget *parent)
    

5.  : QMainWindow(parent), statusLabel(this)
    

6. {
    

7. }
    

8. 9. bool MainWindow::construct()
    

10. {
    

11.  bool ret = true;
    

12.  ret = ret && initMenuBar();
    

13.  ret = ret && initToolBar();
    

14.  ret = ret && initStatusBar();
    

15.  ret = ret && initinitMainEditor();
    

16.  return ret;
    

17. }
    

18. MainWindow* MainWindow::NewInstance()
    

19. {
    

20.  MainWindow* ret = new MainWindow();
    

21. 22.  if((ret==NULL) || (!ret->construct()))
    

23.  {
    

24.  delete ret;
    

25.  ret = NULL;
    

26.  }
    

27. 28.  return ret;
    

29. }
    

30.  bool MainWindow::initMenuBar()//Menu bar
    

31. {
    

32.  bool ret = true;
    

33. 34.  QMenuBar* mb = menuBar();//Be sure to pay attention to menuBar(), which is an ordinary member function, not a constructor
    

35. 36.  ret = ret && initFileMenu(mb);//Passing a parameter is to add the menu to the menu bar in the initFileMenu() function
    

37.  ret = ret && initEditMenu(mb);
    

38.  ret = ret && initFormatMenu(mb);
    

39.  ret = ret && initViewMenu(mb);
    

40.  ret = ret && initHelpMenu(mb);
    

41. 42.  return ret;
    

43. 44. }
    

45. 46.  bool MainWindow::initToolBar()//Toolbar
    

47. {
    

48.  bool ret = true;
    

49. 50.  QToolBar* tb = addToolBar("Tool Bar");
    

51.  //tb->setMovable(false);
    

52.  //tb->setFloatable(false);
    

53.  tb->setIconSize(QSize(16,16));
    

54. 55.  ret = ret && initFileToolItem(tb);
    

56.  tb->addSeparator();
    

57.  ret = ret && initEditToolItem(tb);
    

58.  tb->addSeparator();
    

59.  ret = ret && initFormatToolItem(tb);
    

60.  tb->addSeparator();
    

61.  ret = ret && initViewToolItem(tb);
    

62. 63.  return ret;
    

64. }
    

65. 66.  bool MainWindow::initStatusBar()//Status bar
    

67. {
    

68.  bool ret = true;
    

69. 70.  QStatusBar* sb = statusBar();
    

71. 72.  QLabel* label = new QLabel("Made By LGC");
    

73. 74.  if(label != NULL)
    

75.  {
    

76.  statusLabel.setMinimumWidth(200);
    

77.  statusLabel.setAlignment(Qt::AlignHCenter);
    

78.  statusLabel.setText("Ln:1 Col:1");
    

79. 80. 81.  label->setMinimumWidth(200);
    

82.  label->setAlignment(Qt::AlignHCenter);
    

83. 84.  sb->addPermanentWidget(new QLabel());//Just add the separator
    

85.  sb->addPermanentWidget(&statusLabel);
    

86.  sb->addPermanentWidget(label);
    

87.  }
    

88.  else
    

89.  {
    

90.  ret = false;
    

91.  }
    

92.  return ret;
    

93. }
    

94.  bool MainWindow::initinitMainEditor()//Edit window
    

95. {
    

96.  bool ret = true;
    

97. 98.  mainEdit.setParent(this);
    

99.  setCentralWidget(&mainEdit);
    

100. 101.  return ret;
    

102. }
    

103. 104.  /************************************************file menu************************************************* *******/
    

105. bool MainWindow::initFileMenu(QMenuBar* mb)
    

106. {
    

107.  bool ret = true;
    

108. 109.  QMenu* menu = new QMenu("File(&F)");//Create a file menu, (&F) is to open it with Alt+F
    

110.  ret = (menu != NULL);
    

111.  if(ret)
    

112.  {
    

113.  QAction* action = NULL;
    

114. 115.  //New
    

116.  ret = ret && makeAction(action, menu, "New(&N)",Qt::CTRL + Qt::Key_N);
    

117.  if(ret)
    

118.  {
    

119.  menu->addAction(action);
    

120.  }
    

121. 122.  menu->addSeparator();
    

123. 124.  //Open
    

125.  ret = ret && makeAction(action, menu,"Open(&O)...",Qt::CTRL + Qt::Key_O);
    

126.  if(ret)
    

127.  {
    

128.  menu->addAction(action);
    

129.  }
    

130. 131.  menu->addSeparator();
    

132. 133.  //Save
    

134.  ret = ret && makeAction(action, menu,"Save(&S)",Qt::CTRL + Qt::Key_S);
    

135.  if(ret)
    

136.  {
    

137.  menu->addAction(action);
    

138.  }
    

139. 140.  menu->addSeparator();
    

141. 142.  //Save As
    

143.  ret = ret && makeAction(action, menu, "Save As(&A)...",0);
    

144.  if(ret)
    

145.  {
    

146.  menu->addAction(action);
    

147.  }
    

148. 149.  menu->addSeparator();
    

150. 151.  //print
    

152.  ret = ret && makeAction(action, menu, "Print(&P)...",Qt::CTRL + Qt::Key_P);
    

153.  if(ret)
    

154.  {
    

155.  menu->addAction(action);
    

156.  }
    

157. 158.  menu->addSeparator();
    

159. 160.  //Exit
    

161.  ret = ret && makeAction(action, menu,"Exit(&X)",0);
    

162.  if(ret)
    

163.  {
    

164.  menu->addAction(action);//Add menu items to the menu
    

165.  }
    

166. 167.  }
    

168.  if(ret)
    

169.  {
    

170.  mb->addMenu(menu);//Add the menu to the menu bar
    

171.  }
    

172.  else
    

173.  {
    

174.  delete mb;
    

175.  }
    

176.  return ret;
    

177. }
    

178. 179.  /************************************************edit menu************************************************* *******/
    

180. bool MainWindow::initEditMenu(QMenuBar* mb)
    

181. {
    

182.  bool ret = true;
    

183. 184.  QMenu* menu = new QMenu("Edit(&E)");
    

185.  ret = (menu != NULL);
    

186.  if(ret)
    

187.  {
    

188.  QAction* action = NULL;
    

189. 190.  //Undo
    

191.  ret = ret && makeAction(action, menu,"Undo(&U)",Qt::CTRL + Qt::Key_Z);
    

192.  if(ret)
    

193.  {
    

194.  menu->addAction(action);
    

195.  }
    

196. 197.  menu->addSeparator();
    

198. 199.  //Redo
    

200.  ret = ret && makeAction(action, menu,"Redo(&R)...",Qt::CTRL + Qt::Key_Y);
    

201.  if(ret)
    

202.  {
    

203.  menu->addAction(action);
    

204.  }
    

205. 206.  menu->addSeparator();
    

207. 208.  //Cut
    

209.  ret = ret && makeAction(action, menu,"Cut(&T)",Qt::CTRL + Qt::Key_X);
    

210.  if(ret)
    

211.  {
    

212.  menu->addAction(action);
    

213.  }
    

214. 215.  menu->addSeparator();
    

216. 217.  //Copy
    

218.  ret = ret && makeAction(action, menu,"Copy(&C)...",Qt::CTRL + Qt::Key_C);
    

219.  if(ret)
    

220.  {
    

221.  menu->addAction(action);
    

222.  }
    

223. 224.  menu->addSeparator();
    

225. 226.  //Pase
    

227.  ret = ret && makeAction(action, menu,"Pase(&P)...",Qt::CTRL + Qt::Key_V);
    

228.  if(ret)
    

229.  {
    

230.  menu->addAction(action);
    

231.  }
    

232. 233.  menu->addSeparator();
    

234. 235.  //Delete
    

236.  ret = ret && makeAction(action, menu, "Delete(&L)",Qt::Key_Delete);
    

237.  if(ret)
    

238.  {
    

239.  menu->addAction(action);
    

240.  }
    

241. 242.  menu->addSeparator();
    

243. 244.  //Find
    

245.  ret = ret && makeAction(action, menu,"Find(&F)...",Qt::CTRL + Qt::Key_F);
    

246.  if(ret)
    

247.  {
    

248.  menu->addAction(action);
    

249.  }
    

250. 251.  menu->addSeparator();
    

252. 253.  //Replace
    

254.  ret = ret && makeAction(action, menu,"Replace(&R)...",Qt::CTRL + Qt::Key_H);
    

255.  if(ret)
    

256.  {
    

257.  menu->addAction(action);
    

258.  }
    

259. 260.  menu->addSeparator();
    

261. 262.  //Goto
    

263.  ret = ret && makeAction(action, menu,"Goto(&G)",Qt::CTRL + Qt::Key_G);
    

264.  if(ret)
    

265.  {
    

266.  menu->addAction(action);
    

267.  }
    

268. 269.  menu->addSeparator();
    

270. 271.  //Select All
    

272.  ret = ret && makeAction(action, menu, "Select All(&A)",Qt::CTRL + Qt::Key_A);
    

273.  if(ret)
    

274.  {
    

275.  menu->addAction(action);
    

276.  }
    

277. 278.  }
    

279.  if(ret)
    

280.  {
    

281.  mb->addMenu(menu);
    

282.  }
    

283.  else
    

284.  {
    

285.  delete mb;
    

286.  }
    

287.  return ret;
    

288. }
    

289. 290.  /************************************************format menu************************************************* *******/
    

291. bool MainWindow::initFormatMenu(QMenuBar* mb)
    

292. {
    

293.  bool ret = true;
    

294. 295.  QMenu* menu = new QMenu("Format(&O)");
    

296.  ret = (menu != NULL);
    

297.  if(ret)
    

298.  {
    

299.  QAction* action = NULL;
    

300. 301.  //Auto Wrap
    

302.  ret = ret && makeAction(action, menu,"Auto Wrap(&W)",0);
    

303.  if(ret)
    

304.  {
    

305.  menu->addAction(action);
    

306.  }
    

307. 308.  menu->addSeparator();
    

309. 310.  //Font
    

311.  ret = ret && makeAction(action, menu,"Font(&F)...",0);
    

312.  if(ret)
    

313.  {
    

314.  menu->addAction(action);
    

315.  }
    

316. 317.  }
    

318.  if(ret)
    

319.  {
    

320.  mb->addMenu(menu);
    

321.  }
    

322.  else
    

323.  {
    

324.  delete mb;
    

325.  }
    

326.  return ret;
    

327. }
    

328. 329.  /************************************************view menu************************************************* *******/
    

330. bool MainWindow::initViewMenu(QMenuBar* mb)
    

331. {
    

332.  bool ret = true;
    

333. 334.  QMenu* menu = new QMenu("View(&V)");
    

335.  ret = (menu != NULL);
    

336.  if(ret)
    

337.  {
    

338.  QAction* action = NULL;
    

339. 340.  //Tool Bar
    

341.  ret = ret && makeAction(action, menu,"Tool Bar(&T)",0);
    

342.  if(ret)
    

343.  {
    

344.  menu->addAction(action);
    

345.  }
    

346. 347.  menu->addSeparator();
    

348. 349.  //Status Bar
    

350.  ret = ret && makeAction(action, menu,"Status Bar(&S)",0);
    

351.  if(ret)
    

352.  {
    

353.  menu->addAction(action);
    

354.  }
    

355. 356.  }
    

357.  if(ret)
    

358.  {
    

359.  mb->addMenu(menu);
    

360.  }
    

361.  else
    

362.  {
    

363.  delete mb;
    

364.  }
    

365.  return ret;
    

366. }
    

367. 368.  /************************************************help menu************************************************* *******/
    

369. bool MainWindow::initHelpMenu(QMenuBar* mb)
    

370. {
    

371.  bool ret = true;
    

372. 373.  QMenu* menu = new QMenu("Help(&H)");
    

374.  ret = (menu != NULL);
    

375.  if(ret)
    

376.  {
    

377.  QAction* action = NULL;
    

378. 379.  //User Manual
    

380.  ret = ret && makeAction(action, menu,"User Manual",0);
    

381.  if(ret)
    

382.  {
    

383.  menu->addAction(action);
    

384.  }
    

385. 386.  menu->addSeparator();
    

387. 388.  //About NotePad
    

389.  ret = ret && makeAction(action, menu,"About NotePad...",0);
    

390.  if(ret)
    

391.  {
    

392.  menu->addAction(action);
    

393.  }
    

394. 395.  }
    

396.  if(ret)
    

397.  {
    

398.  mb->addMenu(menu);
    

399.  }
    

400.  else
    

401.  {
    

402.  delete mb;
    

403.  }
    

404.  return ret;
    

405. }
    

406.  /*****************************************tool******* ************************************************** ***/
    

407. bool MainWindow::initFileToolItem(QToolBar* tb)
    

408. {
    

409.  bool ret = true;
    

410.  QAction* action = NULL;
    

411. 412.  ret = ret && makeAction(action, tb, "New", ":/Res/pic/new.png");
    

413.  if(ret)
    

414.  {
    

415.  tb->addAction(action);
    

416. 417.  }
    

418. 419.  ret = ret && makeAction(action, tb,"Open", ":/Res/pic/open.png");
    

420.  if(ret)
    

421.  {
    

422.  tb->addAction(action);
    

423.  }
    

424. 425.  ret = ret && makeAction(action, tb,"Save", ":/Res/pic/save.png");
    

426.  if(ret)
    

427.  {
    

428.  tb->addAction(action);
    

429.  }
    

430. 431.  ret = ret && makeAction(action, tb,"Save As", ":/Res/pic/saveas.png");
    

432.  if(ret)
    

433.  {
    

434.  tb->addAction(action);
    

435.  }
    

436.  ret = ret && makeAction(action, tb,"Print", ":/Res/pic/print.png");
    

437.  if(ret)
    

438.  {
    

439.  tb->addAction(action);
    

440.  }
    

441.  return ret;
    

442. 443. }
    

444. bool MainWindow::initEditToolItem(QToolBar* tb)
    

445. {
    

446.  bool ret = true;
    

447.  QAction* action = NULL;
    

448. 449.  ret = ret && makeAction(action, tb,"Undo", ":/Res/pic/undo.png");
    

450.  if(ret)
    

451.  {
    

452.  tb->addAction(action);
    

453.  }
    

454.  ret = ret && makeAction(action, tb,"Redo", ":/Res/pic/redo.png");
    

455.  if(ret)
    

456.  {
    

457.  tb->addAction(action);
    

458.  }
    

459. 460.  ret = ret && makeAction(action, tb, "Cut", ":/Res/pic/cut.png");
    

461.  if(ret)
    

462.  {
    

463.  tb->addAction(action);
    

464.  }
    

465. 466.  ret = ret && makeAction(action, tb,"Copy", ":/Res/pic/copy.png");
    

467.  if(ret)
    

468.  {
    

469.  tb->addAction(action);
    

470.  }
    

471. 472.  ret = ret && makeAction(action, tb,"Paste", ":/Res/pic/paste.png");
    

473.  if(ret)
    

474.  {
    

475.  tb->addAction(action);
    

476.  }
    

477. 478.  ret = ret && makeAction(action, tb,"Find", ":/Res/pic/find.png");
    

479.  if(ret)
    

480.  {
    

481.  tb->addAction(action);
    

482.  }
    

483.  ret = ret && makeAction(action, tb,"Replace", ":/Res/pic/replace.png");
    

484.  if(ret)
    

485.  {
    

486.  tb->addAction(action);
    

487.  }
    

488.  ret = ret && makeAction(action, tb,"Goto", ":/Res/pic/goto.png");
    

489.  if(ret)
    

490.  {
    

491.  tb->addAction(action);
    

492.  }
    

493. 494.  return ret;
    

495. }
    

496. bool MainWindow::initFormatToolItem(QToolBar* tb)
    

497. {
    

498.  bool ret = true;
    

499.  QAction* action = NULL;
    

500. 501.  ret = ret && makeAction(action, tb, "Auto Wrap", ":/Res/pic/wrap.png");
    

502.  if(ret)
    

503.  {
    

504.  tb->addAction(action);
    

505.  }
    

506.  ret = ret && makeAction(action, tb,"Font", ":/Res/pic/font.png");
    

507.  if(ret)
    

508.  {
    

509.  tb->addAction(action);
    

510.  }
    

511. 512.  return ret;
    

513. }
    

514. bool MainWindow::initViewToolItem(QToolBar* tb)
    

515. {
    

516.  bool ret = true;
    

517.  QAction* action = NULL;
    

518. 519.  ret = ret && makeAction(action, tb,"Tool Bar", ":/Res/pic/tool.png");
    

520.  if(ret)
    

521.  {
    

522.  tb->addAction(action);
    

523.  }
    

524.  ret = ret && makeAction(action, tb,"Status Bar", ":/Res/pic/status.png");
    

525.  if(ret)
    

526.  {
    

527.  tb->addAction(action);
    

528.  }
    

529. 530.  return ret;
    

531. }
    

532. 533. 534.  bool MainWindow::makeAction(QAction*& action,QMenu* menu, QString text, int key)//menu item
    

535. {
    

536.  bool ret = true;
    

537.  action = new QAction(text, menu);
    

538.  if(action != NULL)
    

539.  {
    

540.  action->setShortcut(QKeySequence(key));//Create shortcut key
    

541.  }
    

542.  else
    

543.  {
    

544.  ret = false;
    

545.  }
    

546. 547.  return ret;
    

548. }
    

549. bool MainWindow::makeAction(QAction*& action,QToolBar* tb, QString tip, QString icon)
    

550. {
    

551.  bool ret = true;
    

552.  action = new QAction("", tb);
    

553.  if(action != NULL)
    

554.  {
    

555.  action->setToolTip(tip);
    

556.  action->setIcon(QIcon(icon));
    

557.  }
    

558.  else
    

559.  {
    

560.  ret = false;
    

561.  }
    

562.  return ret;
    

563. }
    

564. MainWindow::~MainWindow()
    

565. {
    

566. 567. }
    

568. 569. MainWindow.cpp
    
    

![](/md_blog/public/assets/2021-07-25/d2b88b779cfe3245b75c40ea465a4ccd.gif) main.cpp
    

1. #include <QtGui/QApplication>
    

2. #include "MainWindow.h"
    

3. int main(int argc, char *argv[])
    

4. {
    

5.  QApplication a(argc, argv);
    

6.  MainWindow* w = MainWindow::NewInstance();
    

7.  int ret = -1;
    

8.  if(w != NULL)
    

9.  {
    

10.  w->show();
    

11.  ret = a.exec();
    

12.  }
    

13. 14.  delete w;
    

15.  return ret;
    

16. }
    

17. 18. main.cpp
    
    

# 2\. Summary

(1) The software development process is a series of rules followed by the development team

(2) The significance of the software development process is to ensure the quality and progress of the product

(3) A variety of development process models already exist in the industry

(4) Each software development process has a specific scope of application

(5) The incremental model is used in the curriculum for project development